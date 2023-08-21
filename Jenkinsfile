pipeline {
    agent any

    stages {
        stage('https://github.com/sardaralii/hello.git') {
            steps {
                // Checkout your code from version control here
                // For example:
                // git 'https://github.com/yourusername/your-node-app.git'
            }
        }
        
        stage('Local Build and Run') {
            steps {
                sh 'npm install'
                sh 'npm start'
            }
        }
        
        stage('Docker Build and Run') {
            steps {
                sh 'docker build -t node-hello-world:latest .'
                sh 'docker run -it -p 8080:8080 --name node-hello-world node-hello-world:latest'
            }
        }
    }
}
