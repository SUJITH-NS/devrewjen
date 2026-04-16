pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/SUJITH-NS/devrewjen.git'
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t sujith1ns/devops-html .'
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push sujith1ns/devops-html'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                echo "Stopping old container..."
                docker stop devops-container || true

                echo "Removing old container..."
                docker rm devops-container || true

                echo "Running new container..."
                docker run -d -p 8082:80 --name devops-container sujith1ns/devops-html
                '''
            }
        }
    }
}
