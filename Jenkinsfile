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
                sh "docker build . -t champ3783/notes-app-jenkins:1"
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
                sh "docker image tag notes-app-jenkins:1 ${env.dockeruser}/notes-app-jenkins:1"
                sh "docker login -u ${env.dockeruser} -p ${env.dockerpass}"
                sh "docker push ${env.dockeruser}/notes-app-jenkins:1"
                }
            }
        }
        
        stage("Deploy"){
            steps{
                sh "docker run -itd champ3783/notes-app-jenkins:1"
            }
        }
    }
}
