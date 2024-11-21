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
                git url: 'https://github.com/akshayeanil/2244_ica2_.git', branch: 'develop', credentialsId: 'GIT'
            }
        }

        stage('Build and run docker image') {
            steps {
                sh 'sudo docker build -t akshayeanil/myapp:latest .'
                sh "sudo docker tag akshayeanil/myapp:latest akshayeanil/myapp:develop-${env.BUILD_ID}" 
                sh 'sudo docker run -d -p 8081:80 akshayeanil/myapp:latest'
            } 
        }


        stage('Build and Push') {
            steps {
                echo 'Building..'
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-auth', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                        sh '''
                            sudo docker login -u ${USERNAME} -p ${PASSWORD}
                            sudo docker push akshayeanil/myapp:latest
                        '''
                        sh "sudo docker push akshayeanil/myapp:develop-${env.BUILD_ID}"
                    }
            }
        }

        stage('testing') {
            steps {
                sh 'curl -I 192.168.219.163:8081'
            }
        }

    
    }
}
