pipeline {
    agent any

    environment {
        DOCKER_HUB_USERNAME = 'rabinktm'
        DOCKER_HUB_PASSWORD = 'Avionics@123'
        DOCKER_HUB_REPO = 'rabinktm/sample1'
        IMAGE_NAME = 'hello-world'
    }

    stages {
        stage('Pull Docker Image') {
            steps {
                script {
                    echo "Pulling the hello-world Docker image..."
                    sh "docker pull ${IMAGE_NAME}"
                }
            }
        }

        stage('Tag Docker Image') {
            steps {
                script {
                    echo "Tagging the Docker image for pushing to Docker Hub..."
                    sh "docker tag ${IMAGE_NAME} ${DOCKER_HUB_REPO}:latest"
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    echo "Logging into Docker Hub..."
                    sh "echo ${DOCKER_HUB_PASSWORD} | docker login -u ${DOCKER_HUB_USERNAME} --password-stdin"

                    echo "Pushing the Docker image to Docker Hub..."
                    sh "docker push ${DOCKER_HUB_REPO}:latest"
                }
            }
        }
    }

    post {
        always {
            script {
                echo "Cleaning up local Docker images..."
                sh "docker rmi ${IMAGE_NAME} ${DOCKER_HUB_REPO}:latest"
            }
        }
    }
}
