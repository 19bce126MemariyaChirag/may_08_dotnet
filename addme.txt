pipeline {
    agent any

    stages {
        stage('Build ASP.NET App') {
            steps {
                sh 'docker build -t myapp:latest .'
            }
        }
        
        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-token', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                }
                sh 'docker tag myapp:latest memariyachirag126/myapp:latest'
                sh 'docker push memariyachirag126/myapp:latest'
            }
        }
    }
}
