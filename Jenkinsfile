pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                }
            }
            steps {
                sh '''
                ls -la
                node --version
                npm --version
                npm i react-scripts
                npm run build
                '''
            }
        }

        stage('Test') {
            agent {
                docker {
                    image 'node:18-alpine'
                }
            }
            steps {
                sh '''
                ls -la
                node --version
                npm --version
                npm test
                '''
            }
        }
    }
}