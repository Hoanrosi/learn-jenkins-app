pipeline {
    agent any

    environment {
        NETLIFY_SIDE_ID ='5ba54f49-06f7-4277-bc8a-408f9c84a5d3'
        NETLIFY_AUTH_TOKEN = credentials('netlify-token')
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
                    npm run build
                '''
            }
        }

         stage('Test') {
              agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }

            steps {
                sh ''' 
                    test -f build/index.html
                    npm test
                '''
            }
        }

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
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    npm install netlify-cli
                    node_modules/.bin/netlify --version
                    echo "Linking to Netlify site..."
                    node_modules/.bin/netlify link --id=$NETLIFY_SIDE_ID
                    echo "netlify status:"
                    node_modules/.bin/netlify status
                    echo "Deploying to production. Site ID: $NETLIFY_SIDE_ID"
                    node_modules/.bin/netlify deploy --prod --dir=./build
                '''
            }

        }

          
//           stage('Prod E2E') {
//             agent {
//                 docker {
//                     image 'mcr.microsoft.com/playwright:v1.49.0-noble'
//                     reuseNode true
//                 }
//             }
//             steps {
//                 sh '''
//                     npm install serve
//                     node_modules/.bin/serve -s build &
//                     sleep 10
//                     npx playwright test --reporter=html
//                 '''
//             }
//             post {
//                 always {
//                     pusblishHTML([allMissing: false, alwaysLinkToLastBuild: false, keppAll: false, reporDir: 'playwright-report', reportFiles: 'index.html', reportName: 'Playwright E2E', reportTitles: '', useWrapperFileDirctly: true
// ])
//                 }
//             }
//         }


    }
}
