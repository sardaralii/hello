pipeline {
    agent any
    
    stages {
        stage("clone code") {
            steps {
                echo "Cloning the code"
                git url: "https://github.com/sardaralii/hello.git", branch: "main"
            }
        }
        
        stage("build") {
            steps {
                echo "Building the image"
                sh "docker build -t node-hello-world:latest ."
                sh "docker run -it -p 8080:8080 --name node-hello-world node-hello-world:latest"
"
            }
        }
        
        stage("push to docker hub") {
            steps {
                echo "Pushing to Docker Hub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubuser")]){
                sh "docker tag node-hello-world:latest ${env.dockerHubUser}/node-hello-world:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/node-hello-world:latest"
                }
            }
        }
    }
}
