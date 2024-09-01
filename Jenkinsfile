pipeline {
    agent any

    environment {
        DOCKER_HUB_CREDENTIALS = credentials('your-docker-hub-credentials-id') // Replace with your Jenkins credentials ID
        DOCKER_HUB_REPO = 'rabinktm/sample1'
    }

    stages {
        stage('Pull Docker Image') {
            steps {
                script {
                    echo "Pulling the hello-world image from Docker Hub..."
                    sh 'docker pull hello-world'
                }
            }
        }

        stage('Tag Docker Image') {
            steps {
                script {
                    echo "Tagging the image for pushing to Docker Hub..."
                    sh "docker tag hello-world ${env.DOCKER_HUB_REPO}:latest"
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    echo "Pushing the tagged image to Docker Hub..."
                    sh "echo ${DOCKER_HUB_CREDENTIALS_PSW} | docker login -u ${DOCKER_HUB_CREDENTIALS_USR} --password-stdin"
                    sh "docker push ${env.DOCKER_HUB_REPO}:latest"
                }
            }
        }
    }

    post {
        always {
            script {
                echo "Cleaning up local Docker images..."
                sh "docker rmi hello-world ${env.DOCKER_HUB_REPO}:latest"
            }
        }
    }
}

