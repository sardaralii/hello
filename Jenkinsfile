pipeline {
    agent any
    
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
    }

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/sardaralii/hello.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    def imageName = "yourusername/your-nodejs-app:latest"
                    def dockerFile = "path/to/Dockerfile"  // Specify the path to your Dockerfile
                    docker.build(imageName, "-f ${dockerFile} .")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'dockerhub', variable: 'DOCKERHUB_CREDENTIALS_PSW')]) {
                        sh "echo '\$DOCKERHUB_CREDENTIALS_PSW' | docker login -u '\$DOCKERHUB_CREDENTIALS_USR' --password-stdin"
                        def imageName = "yourusername/your-nodejs-app:latest"
                        sh "docker push ${imageName}"
                    }
                }
            }
        }
    }

    post {
        always {
            sh 'docker logout'
        }
    }
}
