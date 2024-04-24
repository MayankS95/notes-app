pipeline {
    agent any
    
    stages {
        stage(" clone code"){
            steps {
                echo "cloning the code"
                git url: "https://github.com/MayankS95/notes-app.git" , branch: "main"
                
            }
            
        }
        stage("build"){
            steps {
                echo "building the image"
                sh "docker build -t notes-app ."
            }
            
        }
        stage("push"){
            steps {
                echo "pushing the image to the docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerHub" ,passwordVariable:"dockerHubpass" ,usernameVariable:"dockerHubuser")]){
                    sh "docker tag notes-app ${env.dockerHubuser}/notes-app:latest"
                    sh "docker login -u ${env.dockerHubuser} -p ${env.dockerHubpass}"
                    sh "docker push ${env.dockerHubuser}/notes-app:latest"
                }
            
            
                
            }
            
        }
        stage("deploy"){
            steps {
                echo "deploying the image"
                sh "docker-compose down && docker-compose up -d"
            }
            
        }
    }
}
