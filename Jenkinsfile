pipeline {
    agent any

    environment {
        BACKEND_IMAGE = 'myapp-backend:latest'
        FRONTEND_IMAGE = 'myapp-frontend:latest'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/your-username/your-repo.git'
            }
        }

        stage('Build Backend') {
            steps {
                dir('services-test') {
                    sh 'docker build -t $BACKEND_IMAGE .'
                }
            }
        }

        stage('Build Frontend') {
            steps {
                dir('ui-test') {
                    sh 'docker build -t $FRONTEND_IMAGE .'
                }
            }
        }

        stage('Deploy with Docker Compose') {
            steps {
                sh 'docker-compose down || true'
                sh 'docker-compose up -d'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
    }
}
