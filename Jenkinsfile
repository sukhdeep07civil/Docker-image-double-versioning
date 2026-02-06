pipeline {
    agent any

    environment{
        IMAGE_NAME= "ssm0712/jenkins-docker-nginx-app"
        TAG= "${BUILD_NUMBER}"
    }

    stages{
        stage('Docker Login'){
            steps{
                withCredentials([usernamePassword(
                    credentialsId: "dockerhub-creds",
                    usernameVariable: "DOCKER_USER",
                    passwordVariable: "DOCKER_PASS"
                )]){
                    bat 'docker login -u %DOCKER_USER% -p %DOCKER_PASS%'

                }

            }
        }

        stage('Build Docker Image'){
            steps{
                bat ' docker build -t %IMAGE_NAME%:%TAG% -t %IMAGE_NAME%:latest .'
            }
        }

        stage('Push Versioned Image'){
            steps{
                bat 'docker push %IMAGE_NAME%:%TAG%'
            }
        }

        stage('Push Latest Image'){
            steps{
                bat 'docker push %IMAGE_NAME%:latest'
            }
        }
    }
}