pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "umutcoskun/html-web-app"
        DOCKER_TAG = "v1.0"
    }

    stages {
        stage('Pull Docker Image') {
            steps {
                script {
                    sh "docker pull ${DOCKER_IMAGE}:${DOCKER_TAG}"
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} ."
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    sh "docker push ${DOCKER_IMAGE}:${DOCKER_TAG}"
                }
            }
        }
    }
}
