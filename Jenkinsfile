pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                bat 'echo "Building Docker image..."'
            }
        }
        stage('Push Docker Image') {
            steps {
                bat 'echo "Pushing Docker image to registry..."'
            }
        }
        stage('Deploy to Kubernetes') {	
            steps {
                bat 'echo "Executing deployment to Kubernetes..."'
            }
        }
    }
}