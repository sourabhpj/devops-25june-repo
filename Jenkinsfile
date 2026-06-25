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
        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-devops-id', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                    sh 'docker tag my-nginx-image sourabhpj94/my-nginx-image:latest'
                    sh 'docker push sourabhpj94/my-nginx-image:latest'
                }
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
