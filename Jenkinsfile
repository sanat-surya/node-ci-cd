pipeline {
    agent any
    
    stages{
        stage("Code Cloned"){
            steps{
                git url: "https://github.com/SanketShirke/node-cicd-pipeline.git", branch: "main"
                echo "Code Cloned"
            }
            
        }
        stage("Code Built"){
            steps{
                
                sh "docker build . -t node-app-demo"
                echo "Code Built"
            }
        }
        stage("Code Push To Docker Hub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerhubpass",usernameVariable:"dockerhubuser")]){
                    sh "docker login -u ${env.dockerhubuser} -p ${env.dockerhubpass}"
                    sh "docker tag node-app-demo ${env.dockerhubuser}/node-app-demo:latest"
                    sh "docker push ${env.dockerhubuser}/node-app-demo:latest"
                }
                echo "Code Push to Docker hub"
            }
        }
        stage("Code Deploy"){
            
            steps{
                sh "docker-compose down && docker-compose up -d "
                echo "Code Deploy"
            }
        }
        
    }
}
