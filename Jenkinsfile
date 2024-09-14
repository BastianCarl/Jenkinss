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

                   if[-e ./build/index.html]; then
                        return 0
                    else
                        retur 1
                    fi
                '''
            }
        }
    }
}
