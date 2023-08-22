pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                script {
                    // Manually checkout code from Git repository
                    git branch: 'main', url: 'https://github.com/sardaralii/hello.git'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build Docker image
                sh 'docker build -t node-hello-world:latest .'
            }
        }

        stage('Tag and Push Docker Image') {
            steps {
                script {
                    // Tag Docker image
                    sh 'docker tag node-hello-world:latest sardar112/test-docker:latest'

                    //Login 
                    // sh 'docker login -u $sardar122 -p $SAdabahar123'

                    // Push Docker image to Docker Hub
                    sh 'docker push sardar112/test-docker:latest'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                // Run Docker container
                sh 'docker run -p 8000:8000 --name node-hello-world node-hello-world:latest'
            }
        }
    }
}


