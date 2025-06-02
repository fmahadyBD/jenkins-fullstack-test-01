pipeline {
    agent any

    environment {
        BACKEND_IMAGE = 'myapp-backend:latest'
        FRONTEND_IMAGE = 'myapp-frontend:latest'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/fmahadyBD/jenkins-fullstack-test-01.git'
            }
        }

        stage('Build Backend') {
            steps {
                dir('services-test') {
                    sh 'docker build --no-cache -t $BACKEND_IMAGE .'
                }
            }
        }

        stage('Build Frontend') {
            steps {
                dir('ui-test') {
                    sh 'docker build --no-cache -t $FRONTEND_IMAGE .'
                }
            }
        }

        stage('Clean Up Old Containers') {
            steps {
                sh '''
                    docker rm -f ui-test-container || true
                    docker rm -f services-test-container || true
                    docker rm -f jenkins-fullstack-test-01_postgres_1 || true
                '''
            }
        }

        stage('Deploy with Docker Compose') {
            steps {
                sh 'docker-compose down || true'
                sh 'docker-compose up -d --build'
            }
        }
    }

    post {
        always {
            echo '✅ Pipeline finished and app is running with latest changes.'
        }
    }
}
