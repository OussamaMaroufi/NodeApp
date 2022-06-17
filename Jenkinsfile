pipeline {
    agent {
        node { label 'slavefordocker' }
    }
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
                echo 'Login Completed'
            }
        }
        stage('Push Image to Docker Hub') {
            steps {
                sh 'sudo docker push dockerhubusername/dockerhubreponame:$BUILD_NUMBER'
                echo 'Push Image Completed'
            }
        }
  } //stages
    post {
        always {
            // sh 'docker logout'
            echo 'docker hub loug out ...'
        }
    }
}
