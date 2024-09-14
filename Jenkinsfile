pipeline {
    agent any

    environment {
        NETLIFY_SITE_ID = '1d4f5898-6c80-4169-93b9-8ac288ebdcd9'
    }

    stages {

        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }

        stage('Deploy') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    npm install -g netlify-cli
                    netlify --version
                    echo "Deploying to production. SITE ID: ${NETLIFY_SITE_ID}"
                    netlify deploy --prod --site ${NETLIFY_SITE_ID}
                '''
            }
        }
    }
}
