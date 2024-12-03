pipeline {
    agent any

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
            //  agent {
            //     docker {
            //         image 'node:23.3.0'
            //         reuseNode true
            //     }
            // }
            steps {
                sh '''
                    whoami
                    printenv
                     npm install netlify-cli
                     node_modules/.bin/netlify --version
                '''
            }

        }
    }
}
