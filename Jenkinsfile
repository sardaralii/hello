pipeline {
    agent any

    }

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
    }

    stages {

        stage('gitclone') {
            steps {
                git 'https://github.com/sardaralii/hello.git'
            }
        }

        stage('Build') {
            steps {
                sh 'docker build -t thetips4you/nodeapp_test:latest .'
            }
        }

        stage('Login') {
            steps {
                withCredentials([string(credentialsId: 'sardar112', variable: 'DOCKERHUB_CREDENTIALS_USR'),
                                 string(credentialsId: 'SAdabahar123', variable: 'DOCKERHUB_CREDENTIALS_PSW')]) {
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                }
            }
        }

        stage('Push') {
            steps {
                sh 'docker push thetips4you/nodeapp_test:latest'
            }
        }
    }

    post {
        always {
            sh 'docker logout'
        }
    }

}
