pipeline {
    agent any
    environment {
        APP_NAME = "my-web-dotnet-app"
        APP_PORT = "5000"
        IMAGE_TAG = "latest"
        DOCKER_REGISTRY="memariyachirag126"
        
    }
    stages {
        stage('Build') {
            steps {
                
                // Build the project
                sh 'dotnet build'
            }
        }
        stage('test') {
            steps {
                
                // test the project
                sh 'dotnet test'
            }
        }
        stage('pulbish'){
            steps{
                // Publish the project
                sh 'dotnet publish -c Release -o ./publish'
            }
        }
        stage('Docker Build') {
            steps {
                // Build Docker image
                script {
                    docker.build("${DOCKER_REGISTRY}/${APP_NAME}:${IMAGE_TAG}", "--build-arg APP_PORT=${APP_PORT} .")
                }
            }
        }
        stage('Docker Login and Push') {
            steps {
                // Log in to Docker registry
                withCredentials([usernamePassword(credentialsId: 'docker-token', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                    sh "docker login -u ${DOCKER_USERNAME} -p ${DOCKER_PASSWORD}"
                    sh "docker push ${DOCKER_REGISTRY}/${APP_NAME}:${IMAGE_TAG}"
                }
            }
        }

        stage('SSH to local') {
            //ssh script to login with username and password and run command
            steps {
                sshScript(sshpass -p usernotfound ssh meetshah@172.16.1.123 'sudo docker kill $(sudo docker ps -q) ; sudo docker system prune -f ; sudo docker pull phadkesharanmatrixcomsec/pizza-rest-api:1.0  ; 
    sudo docker run -dp 8000:80 --privileged phadkesharanmatrixcomsec/pizza-rest-api:1.0')
            }
        }
    }
}
