pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }
    stages {
        stage('Test') {
            steps {
                echo 'Testing..'
                sh './mvnw clean test'
            }
        }
        
//         stage('Trial') {
//             steps {
//                  withMaven {
//                     mvn clean
//                 }
//             }
//         }
//          Adding Test Commit
        stage('Build') {
            steps {
                sh './mvnw clean package'
            }
        }       
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                sh './mvnw clean deploy'
            }
        }
    }
    post {
        always {
            junit(
                allowEmptyResults: true, 
                testResults: '**/build/test-results/test/*.xml'
            )
            recordIssues(
                enabledForFailure: true, aggregatingResults: true,
                tools: [java(), checkStyle()]
            )
        }
    }
}
