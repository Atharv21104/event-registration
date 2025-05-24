pipeline {
    agent any

    environment {
        IMAGE_NAME = "event-registration"
        CONTAINER_NAME = "event-container"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Atharv21104/event-registration.git'
            }
        }

        stage('Build Image') {
            steps {
                bat "docker build -t %IMAGE_NAME% ."
            }
        }

        stage('Cleanup Old Container') {
            steps {
                bat "docker rm -f %CONTAINER_NAME% || exit 0"
            }
        }

        stage('Deploy Container') {
            steps {
                bat "docker run -d -p 8080:80 --name %CONTAINER_NAME% %IMAGE_NAME%"
            }
        }
    }

    post {
        success {
            echo "✅ Deployment successful: http://localhost:8090"
        }
        failure {
            echo "❌ Build failed. Check error logs."
        }
    }
}
