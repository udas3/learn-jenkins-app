pipeline {
    agent any

    stages {
        stage('Build') {
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode: true
                }
            }
            steps {
//ls -la to list elements hidden
//npm node --versionS in order to help debugging if necessary
//npm ci to install dependencies (in node_modules directory)
//npm run build to run the build 
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
    }
}
