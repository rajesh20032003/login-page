pipeline {
    agent any

    environment {
        IMAGE_NAME = 'login-page'
        CONTAINER_NAME = 'login-page'
        HOST_PORT = '8088'
        CONTAINER_PORT = '8080'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'git@github.com:rajesh20032003/login-page.git', branch: 'master'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME -f Dockerfile.dev .'
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
                sh '''
                    docker run -d \
                        --name $CONTAINER_NAME \
                        -p $HOST_PORT:$CONTAINER_PORT \
                        -v "$PWD":/app \
                        $IMAGE_NAME
                '''
            }
        }
    }
}


