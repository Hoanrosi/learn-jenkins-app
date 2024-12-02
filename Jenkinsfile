pipeline {
    agent any

    stages {

        /*
        stage('Build') {
            agent {
                docker {
                    image 'node:23.3.0-slim'
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
        */
        stage('E2E') {
            agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.49.0-noble'
                    reuseNode true
                    args '-u root:root'
                }
            }
            steps {
                sh '''
                    npm install -g serve
                    node_modules\serve -s build
                    npx playwright test
                '''
            }
        }
    }
}
