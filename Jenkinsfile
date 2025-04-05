pipeline {
    agent any

    environment {
        COMPOSE_PROJECT_NAME = "flaskdocker"
    }

    stages {
        stage('Build Docker Image') {
            steps {
                echo "🔨 Building Docker image..."
                sh 'docker build -t flask-app-image ./app'
            }
        }

        stage('Run Containers using Docker Compose') {
            steps {
                echo "🚀 Running Docker Compose..."
                sh 'docker-compose up -d'
            }
        }
    }

    post {
        always {
            echo "✅ Build completed."
        }
    }
}
