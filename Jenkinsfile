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
            environment {
                tag_version = "${env.BUILD_ID}"
            }

            steps {
                script {
                    //sh 'sed -i "s/{{tag}}/$tag_version/g" ./k8s/deployment.yaml'
                    //sh "kubectl --kubeconfig=C:/infra/kind-config apply -f ./k8s/deployment.yaml"
                    // Substitui {{tag}} no YAML — usando powershell
                    bat """
                    powershell -Command "(Get-Content ./k8s/deployment.yaml) -replace '{{tag}}', '$env:tag_version' | Set-Content ./k8s/deployment.yaml"
                    """

                    // Aplica via kubectl — atenção: isso assume que o kubectl está no PATH
                    bat 'kubectl --kubeconfig=C:\\infra\\kind-config apply -f ./k8s\\deployment.yaml'
                }
            }
        }
    }
}