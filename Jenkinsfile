pipeline {
    agent {
        docker {
            //image 'node:18-alpine'
            image 'mcr.microsoft.com/playwright:v1.62.0-noble'
            reuseNode true
        }
    }

    stages {
        stage('Build') {
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

        stage('E2E') {
            steps {
                sh '''
                   npm install serve
                   node_modules/.bin/serve -s build & sleep 10
                   npx playwright test
                '''
            }
        }
    }

    post {
        always {
            junit 'jest-results/junit.xml'
        }
    }
}