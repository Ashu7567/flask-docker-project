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

        stage('Run Containers using Docker Compose') {
            steps {
                echo '🚀 Running Docker Compose...'
                sh '''
                    docker-compose down || true
                    docker-compose -f docker-compose.yml up -d
                '''
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
            docker run --rm $IMAGE_NAME pytest
        '''
    }
}


        
    }

    post {
        always {
            echo '✅ Build completed.'
        }
    }
}
