pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Truongcr/user-service.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('user-service-0.0.1-SNAPSHOT:latest')
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    docker.image('user-service-0.0.1-SNAPSHOT:latest').run('-d -p 8081:8080')
                }
            }
        }
    }
}
