pipeline {
    agent any

    environment {
       NETLIFY_SITE_ID = 'efa10e20-a213-4789-944d-385be0880dc1'
    }

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
                if [ -f build/index.html ]; then
                    echo "index.html found"
                else
                    echo "ERROR: index.html missing"
                    exit 1
                fi
                npm test
                '''
            }
        }

         stage('Deploy') {
            agent{
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                 npm install  npm install netlify-cli@20.1.1
                 node_modules/.bin/netlify --version
                 echo "Deploying to Netlify site ID: $NETLIFY_SITE_ID"
                '''
            }
        }
    }
}
