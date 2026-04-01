pipeline {
    agent any

    environment {
        IMAGE_NAME = "your-dockerhub-username/jenkins-demo"
    }

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/Vamsi30-coder/Jenkins-Demo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME% .'
            }
        }

        stage('Login to DockerHub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-cred',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    bat 'echo %PASS% | docker login -u %USER% --password-stdin'
                }
            }
        }

        stage('Push Image') {
            steps {
                bat 'docker push %IMAGE_NAME%'
            }
        }

        stage('Run Container') {
            steps {
                bat 'docker run -d -p 5000:5000 %IMAGE_NAME%'
            }
        }
    }
}
