pipeline {
    
    agent { 
        node{
            label "dev"
            
        }
    }
    
    stages{
        stage("Clone Code"){
            steps{
                git url: "https://github.com/Harshan300/django-notes-app.git", branch: "main"
                echo "Aaj toh Linke"
                echo "Harshan "
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
