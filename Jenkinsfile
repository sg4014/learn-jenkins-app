pipeline {
    agent any

    stages {
        agent {
            docker {
                image 'node:18-alpine'
            }
        }

        stage('Build') {
            steps {
                sh '''
                npm --version
                npm run build
                '''
            }
        }
        stage('Test') {
            steps {
                sh '''
                npm test
                '''
            }
        }
    }
}