pipeline {
    agent any

    stages {

        stage('Clone Repo') {
            steps {
                git 'https://github.com/SUJITH-NS/devrewjen.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t sujith1ns/devops-html .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                sh 'docker push sujith1ns/devops-html'
            }
        }

        stage('Deploy Container') {
            steps {
                sh 'docker run -d -p 8082:80 sujith1ns/devops-html'
            }
        }
    }
}
