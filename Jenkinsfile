pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'git@github.com:rajesh20032003/login-page.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t login-page -f Dockerfile.dev .'
            }
        }

        stage('Stop & Remove Existing Container') {
            steps {
                sh '''
                    docker stop login-page || true
                    docker rm login-page || true
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                    docker run -d --name login-page \
                      -p 8080:8080 \
                      -v "$PWD":/app \
                      login-page
                '''
            }
        }
    }
}

