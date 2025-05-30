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

//ls -la to list elements hidden
//npm node --versionS in order to help debugging if necessary
//npm ci to install dependencies (in node_modules directory)
//   npm ci creates the (temporal and unseen by git) node-modules directory
//npm run build to run the build 
//  npm build creates the (temporal and unseen by git) build directory
//ls again to see generated files after execution
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
        stage('Tests'){
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps{
//npm creates the test-results directory
                sh '''
                test -f build/index.html
                npm test
                '''
            }
        }
    }
//post action. After the stages
    post {
        always{
            junit 'test-results/junit.xml'
        }

    }
}
