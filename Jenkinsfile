pipeline {
    agent any

    stages {
        stage('Build ASP.NET App') {
            steps {
                sh 'docker build -t myapp:latest .'
            }
        }
    }
}
