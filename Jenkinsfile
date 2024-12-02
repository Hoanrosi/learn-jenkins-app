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
                    image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    npm install -g serve
                    serve -s build
                    npx playwright test
                '''
            }
        }
    }

    // post {
    //     always{
    //         junit 'test-results/jnit.xml'
    //     }
    // }
}
