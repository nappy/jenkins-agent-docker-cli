pipeline {
    agent any
    environment {
        dockerImage = ''
    }
    triggers {
        cron('@daily')
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
                        if (env.BRANCH_NAME == 'main') {
                            dockerImage.push('latest')
                        }
                    }
                }
            }
        }
    }
}