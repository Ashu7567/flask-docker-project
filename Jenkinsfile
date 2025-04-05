pipeline {
    agent any

    stages {
        stage('Clone Code') {
            steps {
                git 'https://github.com/Ashu7567/flask-docker-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('flask-app-image')
                }
            }
        }

        stage('Run Container using Compose') {
            steps {
                sh 'docker compose up -d'
            }
        }
    }
}
