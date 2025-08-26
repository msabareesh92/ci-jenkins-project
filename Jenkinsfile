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
                sh '''
                echo "Starting Build Stage"
                echo "Node Version:"
                node --version
                echo "NPM version"
                npm --version

                echo "Listing files"
                ls -la

                echo "Installing Dependencies"
                npm ci

                echo "Running Prod Build"
                npm run build

                echo "Listing workspace content"
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
            steps {
                sh '''
                echo "Test Stage"
                echo "Verify the index.html in build directory"

                if test -f build/index.html; then
                  echo "Index.html found"
                else
                  echo "Index.html not found"
                  exit 1
                fi

                echo "Beginning Test"
                npm test
                '''
            }
        }
    }
}
