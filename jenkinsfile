pipeline {
    agent any

    environment {
        IMAGE_NAME = "login-page"
        CONTAINER_NAME = "login-page-container"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'git@github.com:rajesh20032003/login-page.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop & Remove Existing Container') {
            steps {
                sh '''
                docker stop $CONTAINER_NAME || true
                docker rm $CONTAINER_NAME || true
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -d --name $CONTAINER_NAME -p 8088:80 $IMAGE_NAME'
            }
        }
    
}

