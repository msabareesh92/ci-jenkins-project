pipeline{
    agent any 

    stages{
        stage('Build'){
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

                echo "Installing Depe"
                npm ci

                echo "Running Prod Build"
                npm run build

                echo listing workspace content
                ls -la


                '''
            }
        }

        stage ('Test'){
            steps{
                
                sh 'echo "Test Stage"'
                sh '''
                echo "Verify the index.htm in Build directory"
                if test -f build/index.html;then
                echo "Index.html found"
                else
                echo "Index.html not found"
                exit 1
                fi

                echo "Begining Test"
                npm test


                '''
            }
        }

    }


}