pipeline {
    agent any

    stages {
        stage('Build') {
            agent{
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
         stage('test') {
            agent{
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                ls -la
                if [ -f /build/index.html ]; then
                    echo "index.yaml found"
                else
                    echo "ERROR: index.html missing"
                    exit 1
                fi
                npm test
                '''
            }
        }
    }
}
