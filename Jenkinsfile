pipeline {
    agent any 

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh 'docker build -t my-nginx-image .'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker stop my-nginx-container || true'
                sh 'docker rm my-nginx-container || true'
                sh 'docker run -d --name my-nginx-container -p 8081:80 my-nginx-image'
            }
        }
    }
}
