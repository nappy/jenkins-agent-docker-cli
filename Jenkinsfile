pipeline {
    agent any
    environment {
        dockerImage = ''
    }
    stages {
        stage('Build Image') {
            steps {
                script {
                    dockerImage = docker.build('nyri/jenkins-agent-docker-cli')
                }
            }
        }
        stage('Push Image') {
            steps {
                script {
                    docker.withRegistry('', 'nyri-dockerhub') {
                        dockerImage.push('latest')
                    }
                }
            }
        }
    }
}