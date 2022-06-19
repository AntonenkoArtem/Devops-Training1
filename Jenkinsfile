pipeline {
    agent any
    environment {
    DOCKERHUB_CREDENTIALS = credentials('test-dockerhub')
    }
    stages {
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/AntonenkoArtem/Devops-Training1.git'
            }
        }

        stage('Build docker image') {
            steps {
                sh 'docker build -t antonenkoartem/devops-test:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push antonenkoartem/devops-test:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}
