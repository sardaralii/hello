pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                // Manually checkout code from Git repository
                script {
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

        stage('Run Docker Container') {
            steps {
                // Run Docker container
                sh 'docker run -p 8000:8000 --name node-hello-world node-hello-world:latest'
            }
        }
    }
}
