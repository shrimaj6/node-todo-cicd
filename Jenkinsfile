pipeline {
    
    agent any
    
    stages {
        
         stage("Code") {
             steps {
            git url: "https://github.com/shrimaj6/node-todo-cicd.git" , branch: "master" 
            echo "code clone ho gaya "
        }
    }
         
        
        stage("Build & Test") {
            steps {
                
                sh "docker build -t node-app-test-new ."
                echo "code build bhi ho gaya"
            }
        }
        
        stage("Scan Image") {
            steps {
                echo "Image scanning bhi ho gayi"
            }
        }
        
        stage("Push") {
            steps {
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                  sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                  sh "docker tag node-app-test-new:latest ${env.dockerHubUser}/node-app-test-new:latest"
                  sh "docker push ${env.dockerHubUser}/node-app-test-new:latest "
                  echo "code push bhi ho gaya"
                }
                
            }
            
        }
        
        stage("Deploy") {
            steps {
                
                sh "docker-compose down && docker-compose up -d"
                echo "code deploy bhi ho gaya"
            }
        }
    }
}
