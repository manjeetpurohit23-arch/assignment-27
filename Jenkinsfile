pipeline {
    agent any

    environment {
        // Define any environment variables here
        // For example, node or docker paths if not in PATH
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from the repository
                checkout scm
            }
        }

        stage('Build & Deploy Containers') {
            steps {
                // Assuming Jenkins has Docker & docker-compose installed and the user has permissions
                echo 'Building and starting docker containers...'
                // If using Windows Jenkins node with powershell:
                // powershell 'docker-compose up -d --build'
                // If using Linux:
                sh 'docker-compose up -d --build'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished!'
        }
        success {
            echo 'Successfully deployed the application!'
        }
        failure {
            echo 'Deployment failed. Please check the logs.'
        }
    }
}
