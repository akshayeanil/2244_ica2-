pipeline {
    agent any
    stages {
        stage('Cleanup') {
            steps {
                cleanWs()
            }
        }

        stage('Clone Git Repo') {
            steps {
                checkout scm
            }
        }
        stage('Clone from repository') {
            steps {
                git url: 'https://github.com/akshayeanil/2244_ica2-.git', branch: 'develop'
            }
        }

        
stage('Build and run docker image') {
            steps {
                sh 'docker build -t akshayeanil/staticwebsite:latest .'
                sh 'docker stop myapp || true && docker rm myapp || true'
                sh "docker tag akshayeanil/staticwebsite:latest akshayeanil/staticwebsite:develop-${env.BUILD_ID}" 
                sh 'docker run --name myapp -d -p 8081:80 akshayeanil/staticwebsite:latest'
            } 
        }


        stage('Build and Push') {
            steps {
                echo 'Building..'
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-auth', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                        sh '''
                            docker login -u ${USERNAME} -p ${PASSWORD}
                        '''
                      
                    }
            }
        }
        stage('testing') {
            steps {
                sh 'curl -I 34.204.13.156:8080'
            }
        }
       stage('pushing') {
            steps {
                  sh "docker push akshayeanil/staticwebsite:latest"
                  sh "docker push akshayeanil/staticwebsite:develop-${env.BUILD_ID}"
            }
        }
    
    }
}

