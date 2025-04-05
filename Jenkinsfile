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
            # Stop and remove any running containers and networks
            docker-compose down -v --remove-orphans || true

            # Remove leftover container (if still exists)
            docker rm -f flask-container || true

            # Now bring everything up fresh
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

        stage('Push to DockerHub') {
    steps {
        echo '📦 Pushing Docker Image to DockerHub...'
        withCredentials([usernamePassword(credentialsId: 'docker-hub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
            sh '''
                docker login -u $DOCKER_USER -p $DOCKER_PASS
                docker tag flask-app-image $DOCKER_USER/flask-app:latest
                docker push $DOCKER_USER/flask-app:latest
            '''
        }
    }
}

        stage('Deploy to Server') {
    steps {
        echo '🚀 Deploying to remote server...'
        sh '''
        ssh -o StrictHostKeyChecking=no root@142.93.66.255 << EOF
        docker stop flask-container || true
        docker rm flask-container || true
        docker pull $DOCKER_USER/flask-app:latest
        docker run -d --name flask-container -p 5000:5000 $DOCKER_USER/flask-app:latest
        EOF
        '''
    }
}

    post {
        always {
            echo '✅ Build completed.'
        }
    }
}
