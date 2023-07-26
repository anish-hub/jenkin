pipeline {
    agent any 
        stages {
            stage("Code Clone"){
                steps {
                    git url: "https://github.com/anish-hub/jenkin.git", branch: "develop"
                }
            }
            stage("File Build"){
                steps {
                    sh "docker build -t app-todo ."
                }
            }
            stage("File push"){
                steps {
                    withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerhubpass",usernameVariable:"dockerhubuser")]){
                    sh "docker tag app-todo ${env.dockerhubuser}/todo-app:latest"
                    sh "docker login -u ${env.dockerhubuser} -p ${env.dockerhubpass}"
                    sh "docker push ${env.dockerhubuser}/todo-app:latest"
                    }
                }
                
            }
            stage("Container Deploye"){
                steps {
                    sh "docker-compose down && docker-compose up -d"
                }
            }
        }
    
}
