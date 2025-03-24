pipeline {
    agent any
    environment {
        DOCKER_USER = "knikhil999"
        DOCKER_IMAGE = "${DOCKER_USER}/my-app"
        DOCKER_CREDENTIALS = "dockerhub"
    }
    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/KolkurNikhil/register-app.git'
            }
        }
        stage('Build Jar') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${DOCKER_IMAGE}:latest")
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('', DOCKER_CREDENTIALS) {
                        dockerImage.push("latest")
                    }
                }
            }
        }
    }
}
