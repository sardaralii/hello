pipeline {
    agent any

    environment {
        DOCKER_HUB_USERNAME = credentials('sardar112')
        DOCKER_HUB_PASSWORD = credentials('SAdabahar123')
    }

    stages {
        stage('Checkout Code') {
            steps {
                script {
                    // Manually checkout code from Git repository
                    checkout scm
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build Docker image
                script {
                    def dockerImage = docker.build("node-hello-world:latest")
                }
            }
        }

        stage('Tag and Push Docker Image') {
            steps {
                script {
                    // Tag Docker image
                    dockerImage.tag("sardar112/test-docker:latest")

                    // Authenticate with Docker Hub using environment variables
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', passwordVariable: 'DOCKER_HUB_PASSWORD', usernameVariable: 'DOCKER_HUB_USERNAME')]) {
                        sh 'docker login -u sardar112 -p SAdabahar123'

                        // Push Docker image to Docker Hub
                        sh 'docker push sardar112/test-docker:latest'
                    }
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                // Run Docker container
                script {
                    def containerId = docker.run("-p 8000:8000 -d --name node-hello-world sardar112/test-docker:latest")
                    echo "Docker container ID: $containerId"
                }
            }
        }
    }

    post {
        always {
            // Clean up Docker resources after the pipeline completes
            sh 'docker stop node-hello-world || true'
            sh 'docker rm -f node-hello-world || true'
        }
    }
}
