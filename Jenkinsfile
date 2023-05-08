pipeline {
    agent any
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
    }
}
