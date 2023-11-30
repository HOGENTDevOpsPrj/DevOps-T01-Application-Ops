pipeline {
    agent any


    stages {
        stage('Build') {
            steps {
                
                echo "Building.."
                sh "docker compose build"
                }
            }
	
        stage('Test') {
            steps {
                echo "Testing.."
                sh "dotnet restore src/Server/Server.csproj"
                
            }
        }
	stage('Container Down') {
            steps {
                echo 'Docker container down'
                sh "docker compose down"
            }
        }
        stage('Container Up') {
            steps {
                echo 'Docker container up'
                sh "docker compose up -d"
            }
        }

    }
}
