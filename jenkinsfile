pipeline {
    agent any

    stages {
        stage('https://github.com/sardaralii/hello.git') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/sardaralii/hello.git']]])
            }
        }
        
        stage('Build Project') {
            steps {
                sh 'npm install'
            }
        }
        
        stage('Containerize') {
            steps {
                sh 'docker build -t node-hello-world:latest .'
            }
        }
        
        stage('Stop and Remove Container') {
            steps {
                sh 'docker stop node-hello-world || true'
                sh 'docker rm node-hello-world || true'
            }
        }
        
        stage('Run Container') {
            steps {
                sh 'docker run -p 8081:8080 --name node-hello-world node-hello-world:latest'
            }
        }
    }
}
