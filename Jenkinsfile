pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Restore') {
            steps {
                sh 'dotnet restore projectCalculadora.sln'
            }
        }

        stage('Build') {
            steps {
                sh 'dotnet build projectCalculadora.sln --configuration Release'
            }
        }

        stage('Test') {
            steps {
                sh 'dotnet test calculadoraApp.Tests/calculadoraApp.Tests.csproj --configuration Release --no-build'
            }
        }

        stage('Publish') {
            steps {
                sh 'dotnet publish calculadoraApp/calculadoraApp.csproj --configuration Release --output publish'
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'publish/**', fingerprint: true
        }
    }
}
