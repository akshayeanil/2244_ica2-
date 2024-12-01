pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "staticwebsite:latest"
    }
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/akshayeanil/2244_ica2-.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $DOCKER_IMAGE .'
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    sh 'docker push $DOCKER_IMAGE'
                }
            }
        }
    }
    post {
        success {
            echo 'Build and deployment successful for main branch.'
        }
        failure {
            echo 'Build failed for main branch.'
        }
    }
}
