pipeline {
    agent any

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
        stage("Test") {
            steps {
                sh '''
                    if [ -e ./build/index.html ]; then
                        echo "File exists."
                        exit 0
                    else
                        echo "File does not exist."
                        exit 1
                    fi
                '''
            }
        }

    }
}
