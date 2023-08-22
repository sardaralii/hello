pipeline {
    agent any
    
    stages {
        stage('Clone Repository') {
            steps {
                // Clone the repository from your version control system
                git branch: 'main', url: 'https://github.com/yourusername/node-hello-world.git'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                // Build the Docker image using the Dockerfile in the repository
                script {
                    docker.build("node-hello-world:latest", ".")
                }
            }
        }
        
        stage('Run in Container') {
            steps {
                // Run the Docker container
                script {
                    docker.image("node-hello-world:latest").run("-p 8000:8080", "--name node-hello-world")
                }
            }
        }
    }
}
