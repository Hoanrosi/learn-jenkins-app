pipeline {
    agent any

    environment {
        NETLIFY_SIDE_ID ='5ba54f49-06f7-4277-bc8a-408f9c84a5d3'
        NETLIFY_AUTH_TOKEN = credentials('netlify-token')
    }

    stages {

        // stage('E2E') {
        //     agent {
        //         docker {
        //             image 'mcr.microsoft.com/playwright:v1.49.0-noble'
        //             reuseNode true
        //         }
        //     }
        //     steps {
        //         sh '''
        //             npm install serve
        //             node_modules/.bin/serve -s build &
        //             sleep 10
        //             npx playwright test
        //         '''
        //     }
        // }

        stage('Deploy') {
            agent {
                docker {
                    image 'node:23.3.0-slim'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    npm install netlify-cli
                    node_modules/.bin/netlify --version
                    echo "Deploying to production. Site ID: $NETLIFY_SIDE_ID"
                    node_modules/.bin/netlify deploy --dir=build prod
                '''
            }

        }
    }
}
