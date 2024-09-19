pipeline {
    
    agent { 
        node{
            label "dev"
            
        }
    }
    
    stages{
        stage("Clone Code"){
            steps{
                git url: "https://github.com/LondheShubham153/django-notes-app.git", branch: "main"
                echo "Aaj toh LinkedIn Post bannta hai boss"
            }
        }
        stage("Build & Test"){
            steps{
                sh "docker build . -t notes-app:latest"
            }
        }
        stage("Push to DockerHub"){
            steps{
                withCredentials(
                    [usernamePassword(
                        credentialsId:"clicks",
                        passwordVariable:"dockerHubPass", 
                        usernameVariable:"dockerHubUser"
                        )
                    ]
                ){
                sh "docker image tag notes-app:latest ${env.dockerHubUser}/notes-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/notes-app:latest"
                }
            }
        }
        
        stage("Deploy"){
            steps{
                sh "docker compose up -d"
            }
        }
    }
}
