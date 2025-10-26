@Library("shared") _
pipeline {
    agent any;
    stages {
        stage("Code Clone"){
            steps{
                script{
                    clone("https://github.com/AnkitGaurkar/Two_Tier_Application.git", "master")
                }
            }
        }
        stage("Trivy File system scann"){
            steps{
                script{
                    trivy_fs()
                }
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
                script{
                    docker_push("DockerHubCredID", "two-tier-flask-app")
            }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker compose up -d --build flask-app"
            }
        }
    }
    post{
        success{
            script{
                emailext from: 'ankitgaurkar8@gmail.com',
                to: 'ankitgaurkar8@gmail.com,rushikeshtole19@gmail.com',
                    body: 'Build Successfull for CICD Pipeline',
                    subject: "Build for cicd pipeline"
            }
        }
        failure{
            script{
                emailext from: "ankitgaurkar8@gmail.com",
                    to: "ankitgaurkar8@gmail.com,rushikeshtole19@gmail.com",
                    body: "Bad!! Build failed of cicd pipeline",
                    subject: "Build Faild Cicd Pipeline"
            }
        }
    }
}    
