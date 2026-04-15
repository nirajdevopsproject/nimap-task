pipeline {
    agent any

    environment {
        COMPOSE_PROJECT_NAME = "fastapi-devops"
    }

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/nirajdevopsproject/nimap-task'
            }
        }

        stage('Verify Files') {
            steps {
                sh '''
                echo "Listing project files..."
                ls -la
                '''
            }
        }

        stage('Stop Old Containers') {
            steps {
                sh '''
                docker compose down || true
                '''
            }
        }

        stage('Build & Deploy') {
            steps {
                sh '''
                docker compose up -d --build
                '''
            }
        }

        stage('Check Running Containers') {
            steps {
                sh '''
                docker ps
                '''
            }
        }

        stage('Health Check') {
            steps {
                sh '''
                sleep 5
                curl -f http://localhost:8000 || exit 1
                '''
            }
        }
    }

    post {
        success {
            echo 'Deployment Successful!'
        }
        failure {
            echo 'Deployment Failed!'
        }
    }
}
