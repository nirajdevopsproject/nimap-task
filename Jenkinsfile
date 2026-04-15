pipeline {
    agent any

    stages {

        stage('Verify Files') {
            steps {
                sh 'ls -la'
            }
        }

        stage('Stop Old Containers') {
            steps {
                sh 'docker compose down || true'
            }
        }

        stage('Build & Deploy') {
            steps {
                sh 'docker compose up -d --build'
            }
        }

        stage('Check Containers') {
            steps {
                sh 'docker ps'
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
            echo '✅ Deployment Successful!'
        }
        failure {
            echo '❌ Deployment Failed!'
        }
    }
}
