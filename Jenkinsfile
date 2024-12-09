pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "umutcoskun/html-web-app"
        DOCKER_TAG = "v1.0"
        DOCKER_CREDENTIALS = "dockerhub-credentials-id" // Jenkins'te tanımlı kimlik bilgisi ID'si
    }

    stages {
        stage('Pull Docker Image') {
            steps {
                script {
                    echo "Pulling Docker image from Docker Hub..."
                    sh "docker pull ${DOCKER_IMAGE}:${DOCKER_TAG}"
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo "Building new Docker image..."
                    sh "docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} ."
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    echo "Pushing Docker image to Docker Hub..."
                    withCredentials([usernamePassword(credentialsId: env.DOCKER_CREDENTIALS, usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin"
                        sh "docker push ${DOCKER_IMAGE}:${DOCKER_TAG}"
                    }
                }
            }
        }
    }
}
pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "umutcoskun/html-web-app"
        DOCKER_TAG = "v1.0"
        DOCKER_CREDENTIALS = "dockerhub-credentials-id" 
    }

    stages {
        stage('Pull Docker Image') {
            steps {
                script {
                    echo "Pulling Docker image from Docker Hub..."
                    sh "docker pull ${DOCKER_IMAGE}:${DOCKER_TAG}"
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo "Building new Docker image..."
                    sh "docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} ."
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    echo "Pushing Docker image to Docker Hub..."
                    withCredentials([usernamePassword(credentialsId: env.DOCKER_CREDENTIALS, usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin"
                        sh "docker push ${DOCKER_IMAGE}:${DOCKER_TAG}"
                    }
                }
            }
        }
    }
}
