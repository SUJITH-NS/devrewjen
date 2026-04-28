pipeline {
    agent any

    environment {
        IMAGE_NAME = "sujith1ns/devops-html"
        CONTAINER_NAME = "devops-container"
    }

    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/SUJITH-NS/devrewjen.git'
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Login DockerHub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                }
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push $IMAGE_NAME'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker stop $CONTAINER_NAME || true
                docker rm $CONTAINER_NAME || true
                docker run -d -p 8082:80 --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }
    }
}
