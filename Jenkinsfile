pipeline {
    agent any

    stages {
        stage ('build') {
            agent {
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
        stage ('test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }            
            steps {
                sh '''
                    ls -la
                    find -name "build"
                    test -f build/index.html
                    npm test
                '''
                
            }
        }
    }
    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}