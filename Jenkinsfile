pipeline {
    
    agent any
    stages{
        stage("Clone Code"){
            steps{
                git url: "https://github.com/rahat3783/django-notes-project.git", branch: "main"
                echo "Aaj toh LinkedIn Post bannta hai boss"
            }
        }
        stage("Build & Test"){
            steps{
                sh "docker build . -t notes-app-jenkins:latest"
            }
        }
        stage("Push to DockerHub"){
            steps{
                withCredentials(
                    [usernamePassword(
                        credentialsId:"dockerid",
                        passwordVariable:"dockerpass", 
                        usernameVariable:"dockeruser"
                        )
                    ]
                ){
                sh "docker image tag notes-app-jenkins:latest ${env.dockeruser}/notes-app-jenkins:latest"
                sh "docker login -u ${env.dockeruser} -p ${env.dockerpass}"
                sh "docker push ${env.dockeruser}/notes-app-jenkins:latest"
                }
            }
        }
        
        stage("Deploy"){
            steps{
                sh "docker run -itd ${env.dockeruser}/notes-app-jenkins:latest"
            }
        }
    }
}
