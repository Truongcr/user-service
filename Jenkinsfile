pipeline {
    agent any

    environment {
        IMAGE_NAME = "user-service"
        CONTAINER_NAME = "user-service-container"
        PORT = "8080"
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout branch main từ GitHub
                git branch: 'main', url: 'https://github.com/Truongcr/user-service.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh """
                    echo "Building Docker image..."
                    # Xóa image cũ nếu tồn tại
                    if docker images -q \$IMAGE_NAME:latest > /dev/null; then
                        docker rmi -f \$IMAGE_NAME:latest
                    fi
                    docker build -t \$IMAGE_NAME:latest .
                """
            }
        }

        stage('Run Container') {
            steps {
                sh """
                    echo "Running Docker container..."
                    # Xóa container cũ nếu tồn tại
                    if [ \$(docker ps -a -q -f name=\$CONTAINER_NAME) ]; then
                        docker rm -f \$CONTAINER_NAME
                    fi
                    docker run -d --name \$CONTAINER_NAME -p \$PORT:8080 \$IMAGE_NAME:latest
                """
            }
        }
    }

    post {
        success {
            echo "CI/CD pipeline completed successfully!"
        }
        failure {
            echo "CI/CD pipeline failed!"
        }
    }
}
