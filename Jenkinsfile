pipeline {
    agent any

    environment {
        IMAGE_NAME = "flask-app-image"
        CONTAINER_NAME = "flask-app"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                echo '🔨 Building Docker image...'
                sh '''
                    docker build -t $IMAGE_NAME ./app
                '''
            }
        }

        stage('Run Tests') {
            steps {
                echo '🧪 Running Unit Tests...'
                sh '''
                    docker run --rm \
                        -v ${WORKSPACE}/app:/app \
                        -w /app \
                        $IMAGE_NAME \
                        pytest
                '''
            }
        }

        stage('Run Containers using Docker Compose') {
            steps {
                echo '🚀 Running Docker Compose...'
                sh 'docker-compose -f docker-compose.yml up -d'
            }
        }
    }

    post {
        always {
            echo '✅ Build completed.'
        }
    }
}
