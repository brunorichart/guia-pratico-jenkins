pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                sh 'echo "Building Docker image..."'
            }
        }
        stage('Push Docker Image') {
            steps {
                sh 'echo "Pushing Docker image to registry..."'
            }
        }
        stage('Deploy to Kubernetes') {	
            steps {
                sh 'echo "Executing deployment to Kubernetes..."'
            }
        }
    }
}