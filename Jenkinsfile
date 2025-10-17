pipeline {
    agent any

    stages {
        stage("Code clone") {
            steps {
                git url: "https://github.com/AnkitGaurkar/Two_Tier_Application.git", branch: "master"
            }
        }
        stage("Build"){
           steps{
               sh "docker build -t two-tier-flask-app ."
           } 
        }
        stage("Testing"){
            steps{
                echo "Testing done by Tester Team"
            }
        }
        stage("Push to Docker Hub")
        {
            steps{
                withCredentials([usernamePassword(
                    credentialsId: "DockerHubCredID",
                    passwordVariable: "dockerHubPass",
                    usernameVariable: "dockerHubUser"
                    )]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker image tag two-tier-flask-app ${env.dockerHubUser}/two-tier-flask-app"
                sh "docker push ${env.dockerHubUser}/two-tier-flask-app:latest"
            }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker compose up -d --build flask-app"
            }
        }
    }
}
