pipeline {
    agent any

    environment {
        IMAGE_NAME = "brunorichart/guia-jenkins"
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    dockerapp = docker.build("${IMAGE_NAME}:${env.BUILD_ID}", '-f ./src/Dockerfile ./src')
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        dockerapp.push('latest')
                        dockerapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat 'echo Executing deployment to Kubernetes...'
            }
        }
    }
}