pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Truongcr/user-service.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('myapp:latest')
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    docker.image('myapp:latest').run('-d -p 8081:8080')
                }
            }
        }
    }
}
