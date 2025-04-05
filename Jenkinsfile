pipeline {
    agent any

    environment {
        IMAGE_NAME = 'flask-app-image'
    }

    stages {
        stage('Build Docker Image') {
            steps {
                echo '🔨 Building Docker image...'
                sh 'docker build -t $IMAGE_NAME ./app'
            }
        }

        stage('Run Tests') {
            steps {
                echo '🧪 Running Unit Tests...'
                sh 'docker run --rm -v $PWD/app:/app -w /app python:3.9-slim pytest'
            }
        }

        stage('Run Containers using Docker Compose') {
            steps {
                echo '🚀 Running app with Docker Compose...'
                sh 'docker-compose up -d'
            }
        }
    }

    post {
        always {
            echo '✅ Build completed.'
        }
    }
}
