pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker-hub1')
    }
    stages {
        stage('Git Checkout') {
            steps {
                checkout scm

                echo 'checkout the repo '
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'sudo docker build -t oussamamaaroufi/nodeapp:$BUILD_NUMBER .'
                echo 'Build Image Completed'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                // sh 'docker login -u oussamamaaroufi1 -p fEBjP6xYTGxrYC3'
                echo 'Login Completed'
            }
        }
        stage('Push Image to Docker Hub') {
            steps {
                sh 'sudo docker push oussamamaaroufi/nodeapp:$BUILD_NUMBER'
                echo 'Push Image Completed'
            }
        }
    }
    post {
        always {
            // sh 'docker logout'
            echo 'docker hub loug out ...'
        }
    }
}
