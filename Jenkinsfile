pipeline {
    agent any
    
    stages {
        stage('https://github.com/sardaralii/hello.git') {
            steps {
                // Checkout the code from your Git repository
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], userRemoteConfigs: [[url: 'https://github.com/yourusername/your-nodejs-repo.git']]])
            }
        }
        
        stage('Build') {
            steps {
                // Install Node.js dependencies
                sh 'npm install'
            }
        }
        
        stage('Run') {
            steps {
                // Start the Node.js app
                sh 'npm start'
            }
        }
    }
}
