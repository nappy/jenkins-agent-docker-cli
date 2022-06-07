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
                    dockerImage = docker.build('nyri/jenkins-agent-docker-cli', '--pull .')
                }
            }
        }
        stage('Push Image') {
            steps {
                script {
                    docker.withRegistry('', 'dockerhub-nyri') {
                        if (env.BRANCH_NAME == 'main') {
                            dockerImage.push('latest')
                        }
                    }
                }
            }
        }
    }
}