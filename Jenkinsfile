pipeline {
    agent any
    environment {
        DOCKER_USER = "knikhil999"
        DOCKER_IMAGE = "${DOCKER_USER}/my-app"
        DOCKER_CREDENTIALS = "dockerhub"
        MAVEN_HOME = "/opt/maven/bin/mvn"
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/KolkurNikhil/register-app.git'
            }
        }
        stage('Build Jar') {
            steps {
                sh '${MAVEN_HOME} clean package'
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


