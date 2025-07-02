pipeline {
    agent any

    environment {
        IMAGE_NAME = "node-web-app"
        CONTAINER_NAME = "node-web-app-container"
        PORT = "3000"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/asadali2004/node-web-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    bat """docker build -t %IMAGE_NAME%:%BUILD_NUMBER% ."""
                }
            }
        }

        stage('Stop and Remove Old Container') {
            steps {
                script {
                    bat """docker stop %CONTAINER_NAME% || echo Container not running"""
                    bat """docker rm %CONTAINER_NAME% || echo Container not found"""
                }
            }
        }

        stage('Run New Container') {
            steps {
                script {
                    bat """docker run -d --name %CONTAINER_NAME% -p 8081:%PORT% %IMAGE_NAME%:%BUILD_NUMBER%"""
                }
            }
        }
    }
}
