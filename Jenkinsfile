pipeline {
    agent any 
    
    stages {
        stage("Code Clone"){
            steps{
                git url: "https://github.com/SanketShirke/node-cicd-pipeline.git", branch: "main"
                 echo "Code Cloned"
            }
        }
        stage("Code Build"){
            steps{
                sh "docker build . -t node-app"
                 echo "Code Build"
            }
            
        }
        stage("Code Image "){
            steps{
                 withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerhubpass",usernameVariable:"dockerhubuser")]){
                  sh "docker login -u ${env.dockerhubuser} -p ${env.dockerhubpass}"
                  sh "docker tag node-app ${env.dockerhubuser}/node-app:latest"
                  sh " docker push ${env.dockerhubuser}/node-app:latest"
                }
                 echo "Code Test"
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
