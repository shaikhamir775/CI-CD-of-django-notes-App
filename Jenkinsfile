pipeline {
    
    agent any
    stages{
        stage("Clone Code"){
            steps{
                git url: "https://github.com/rahat3783/django-notes-project.git", branch: "main"
                echo "successfully clonning"
            }
        }
        stage("Build & Test"){
            steps{
                sh "docker build . -t notes-app-jenkins:1"
                echo "successfully build and test code"
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
                echo "successfully image pushed to  docker repo"
            }
            
        }
        
        stage("Deploy"){
            steps{
                
                sh "docker run -d -p 8000:8000 --network mynet1 champ3783/notes-app-jenkins:1"
            }
        }
    }
}
