pipeline {
    agent any
    environment {
        IMAGE_NAME = "event-registration"
        CONTAINER_NAME = "event-container"
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-username/event-registration.git'
            }
        }
        stage('Build Image') {
            steps {
                sh "docker build -t $IMAGE_NAME ."
            }
        }
        stage('Cleanup Old Container') {
            steps {
                sh "docker rm -f $CONTAINER_NAME || true"
            }
        }
        stage('Deploy Container') {
            steps {
                sh "docker run -d -p 8080:80 --name $CONTAINER_NAME $IMAGE_NAME"
            }
        }
    }
    post {
        success {
            echo "Application deployed successfully at http://localhost:8080"
        }
    }
}
