pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from the repository
                checkout scm
            }
        }

        stage('Stop Existing Containers') {
            steps {
                echo 'Stopping any previously running containers...'
                // Use "|| true" so the pipeline doesn't fail if no containers are running
                bat 'docker compose down || echo No containers to stop'
            }
        }

        stage('Build & Deploy Containers') {
            steps {
                echo 'Building and starting docker containers...'
                bat 'docker compose up -d --build'
            }
        }

        stage('Verify Running Containers') {
            steps {
                echo 'Checking running containers...'
                bat 'docker compose ps'
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
            bat 'docker compose logs --tail=50 || echo Could not fetch logs'
        }
    }
}
