pipeline {
    agent any

    environment {
        IMAGE_NAME = "flask-app-image"
        DOCKER_REPO = "ashu7567/flask-app:latest"
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
                sh 'docker build -t $IMAGE_NAME ./app'
            }
        }

        stage('Run Containers using Docker Compose') {
            steps {
                echo '🚀 Running Docker Compose...'
                sh '''
                    docker-compose down -v --remove-orphans || true
                    docker rm -f flask-container || true
                    docker-compose -f docker-compose.yml up -d
                '''
            }
        }

        stage('Run Tests') {
            steps {
                echo '🧪 Running Unit Tests...'
                sh 'docker run --rm $IMAGE_NAME pytest'
            }
        }

        stage('Push to DockerHub') {
            steps {
                echo '📦 Pushing Docker Image to DockerHub...'
                withCredentials([usernamePassword(credentialsId: 'docker-hub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                    sh 'docker tag $IMAGE_NAME $DOCKER_REPO'
                    sh 'docker push $DOCKER_REPO'
                }
            }
        }

        stage('Deploy to Server') {
            steps {
                echo '🚀 Deploying to remote server...'
                script {
                    sh """
                    ssh -o StrictHostKeyChecking=no root@142.93.66.255 << EOF
                    docker stop flask-container || true
                    docker rm flask-container || true
                    docker pull $DOCKER_REPO
                    docker run -d --name flask-container -p 5000:5000 $DOCKER_REPO
                    EOF
                }
            }
        }
    }

    post {
        always {
            echo '✅ Build completed.'
        }
    }
}
