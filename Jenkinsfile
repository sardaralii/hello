pipeline {
    agent any

    stages {
        stage('Clone Code') {
            steps {
                git credentialsId: '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', url: 'https://github.com/sardaralii/hello.git'
            }
        }

        stage('Build and Run Locally') {
            steps {
                script {
                    // Install Node.js dependencies and start the app
                    sh 'npm install'
                    sh 'npm start'
                }
            }
        }

        stage('Dockerize and Run') {
            steps {
                script {
                    // Build Docker image
                    sh 'docker build -t node-hello-world:latest .'

                    // Run Docker container
                    sh 'docker run -it -p 8080:8080 --name node-hello-world node-hello-world:latest'
                }
            }
        }
    }

    post {
        always {
            // Clean up Docker resources
            sh 'docker stop node-hello-world'
            sh 'docker rm node-hello-world'
            sh 'docker system prune -af'
        }
    }
}
