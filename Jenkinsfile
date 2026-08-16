pipeline {
    agent any

    environment {
        NETLIFY_SITE_ID = 'ed0ac988-f290-4a50-87d9-5f478110f0e4'
        NETLIFY_AUTH_TOKEN = credentials('netlify-token')
    }

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:22-alpine'
                }
            }
            steps {
                sh '''
                ls -la
                node --version
                npm --version
                npm install
                npm ci
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

        stage('Deploy') {
            agent {
                docker {
                    image 'node:22-alpine'
                }
            }
            steps {
                sh '''
                ls -la
                node --version
                npm --version
                npm install --save-dev netlify-cli
                which netlify
                echo $PATH
                netlify --version
                echo 'Deploying to Project ID: ${NETLIFY_SITE_ID}'
                netlify status
                netlify deploy --dir=build --prod
                '''
            }
        }
    }

    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}