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
                sh "docker build . -t notes-app-jenky:latest"
            }
        }
        stage("Push to DockerHub"){
            steps{
                withCredentials(
                    [usernamePassword(
                        credentialsId:"dockerCreds",
                        passwordVariable:"dockerHubPass", 
                        usernameVariable:"dockerHubUser"
                        )
                    ]
                ){
                sh "docker image tag notes-app-jenky:latest ${env.dockerHubUser}/notes-app-jenky:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/notes-app-jenky:latest"
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
