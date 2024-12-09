pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "umutcskn681/html-web-app"
        DOCKER_TAG = "v1.0"
        DOCKER_CREDENTIALS = "dockerhub-credentials-id"
    }

    stages {
        stage('Login to DockerHub') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: env.DOCKER_CREDENTIALS, usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin"
                    }
                }
            }
        }
        
        stage('Pull Docker Image') {
            steps {
                script {
                    sh "docker pull ${DOCKER_IMAGE}:${DOCKER_TAG}"
                }
            }
        }
    }
}
