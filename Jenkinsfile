pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    if (isUnix()) {
                        sh '''
                        echo "Building on Unix/Linux"
                        ls -la
                        '''
                    } else {
                        bat '''
                        echo Building on Windows
                        dir
                        '''
                    }
                }
            }
        }

        stage('Test') {
            steps {
                echo 'Running simple smoke tests...'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'index.html', allowEmptyArchive: true
            }
        }
    }

    post {
        success {
            echo "SUCCESS: Build completed"
        }
        failure {
            echo "FAILURE: Build failed"
        }
        always {
            cleanWs()
        }
    }
}
