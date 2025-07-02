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
                bat """docker build -t %IMAGE_NAME%:%BUILD_NUMBER% ."""
            }
        }

        stage('Stop and Remove Old Container') {
            steps {
                bat '''
docker stop %CONTAINER_NAME%
IF %ERRORLEVEL% NEQ 0 (
    echo Container not running, continuing...
    EXIT /B 0
)
'''
                bat '''
docker rm %CONTAINER_NAME%
IF %ERRORLEVEL% NEQ 0 (
    echo Container not found, continuing...
    EXIT /B 0
)
'''
            }
        }

        stage('Run New Container') {
            steps {
                bat """docker run -d --name %CONTAINER_NAME% -p 8081:%PORT% %IMAGE_NAME%:%BUILD_NUMBER%"""
            }
        }
    }
}
