pipeline {
    agent any
    stages {
        
stage('Build and run docker image') {
            steps {
                
                sh 'docker stop staticwebsite || true && docker rm staticwebsite || true'
                sh "docker pull akshayeanil/staticwebsite:latest" 
                sh 'docker run --name staticwebsite -d -p 8082:80 akshayeanil/staticwebsite:latest'
            } 
        }


      
        stage('testing') {
            steps {
                sh 'curl -I 107.21.66.204:8082'
            }
        }
      
    }
}
