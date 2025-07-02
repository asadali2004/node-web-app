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
                git 'https://github.com/asadali2004/node-web-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t $IMAGE_NAME:${BUILD_NUMBER} ."
                }
            }
        }

        stage('Stop and Remove Old Container') {
            steps {
                script {
                    sh "docker stop $CONTAINER_NAME || true"
                    sh "docker rm $CONTAINER_NAME || true"
                }
            }
        }

        stage('Run New Container') {
    steps {
        script {
            sh "docker run -d --name $CONTAINER_NAME -p 8081:$PORT $IMAGE_NAME:${BUILD_NUMBER}"
        }
    }
}

    }
}
