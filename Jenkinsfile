pipeline {
  agent any 
    {
        docker {
            image 'mcr.microsoft.com/dotnet/sdk:7.0'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub-token')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t memariyachirag126/jenkins-docker-hub .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push memariyachirag126/jenkins-docker-hub'
      }
    }
    post {
      always {
        sh 'docker logout'
      }
    }
  }
}
