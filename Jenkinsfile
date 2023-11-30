pipeline {
    agent any


    stages {
        stage('Remove Containers') {
            steps {
                script {
                    echo 'Remove Containers'

                    // Check if the 'db' container exists
                    def dbContainerExists = sh(script: 'docker ps -a --format "{{.Names}}" | grep -wq "db"', returnStatus: true)

                    // Remove the 'db' container if it exists
                    if (dbContainerExists == 0) {
                        sh "docker rm -f db"
                        echo 'Container "db" removed'
                    } else {
                        echo 'Container "db" does not exist'
                    }

                    // Check if the 'web' container exists
                    def webContainerExists = sh(script: 'docker ps -a --format "{{.Names}}" | grep -wq "web"', returnStatus: true)

                    // Remove the 'web' container if it exists
                    if (webContainerExists == 0) {
                        sh "docker rm -f web"
                        echo 'Container "web" removed'
                    } else {
                        echo 'Container "web" does not exist'
                    }
                }
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
