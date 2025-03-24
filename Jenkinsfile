pipeline {
    agent any
    environment {
        DOCKER_USER = "knikhil999"
        DOCKER_IMAGE = "${DOCKER_USER}/my-app"
        DOCKER_CREDENTIALS = "dockerhub"
        MAVEN_PATH = "/opt/maven/bin/mvn"  // Define Maven path explicitly
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/KolkurNikhil/register-app.git'
            }
        }
        stage('Build Jar') {
            steps {
                sh '${MAVEN_PATH} clean package'  // Use full Maven path
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



