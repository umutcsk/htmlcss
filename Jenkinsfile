pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "umutcskn681/html-web-app"
        DOCKER_TAG = "v1.0"
        DOCKER_CREDENTIALS = "dockerhub"
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

        stage('SonarQube Analysis') {
            steps {
                script {
                    echo "Running SonarQube analysis..."
                    withSonarQubeEnv('jenkins-sonar') { 
                        sh "mvn clean install sonar:sonar -Dsonar.projectKey=htmlcss"
                    }
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

        stage('Wait for SonarQube Quality Gate') {
            steps {
                script {
                    echo "Waiting for SonarQube Quality Gate..."
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
