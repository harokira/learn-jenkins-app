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

            // npm ci = clean install
            steps {
                sh '''
                    echo "Hello World"
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
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

            // npm ci so that there will be build for the test to work with
            steps {
                sh '''
                    echo "Test Stage"
                    sh "test -f build/index.html"
                    npm ci
                    npm test

                '''
            }
        }
    }
}
