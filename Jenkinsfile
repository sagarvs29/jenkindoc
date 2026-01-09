pipeline {
    agent any

    environment {
        IMAGE_NAME = "dockerhubusername/jenkins-app"
        TAG = "latest"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git 'https://github.com/yourusername/jenkins-docker-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:${TAG}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry(
                        'https://index.docker.io/v1/',
                        'dockerhub-creds'
                    ) {
                        docker.image("${IMAGE_NAME}:${TAG}").push()
                    }
                }
            }
        }
    }
}
