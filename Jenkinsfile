pipeline {

    agent any

    environment {
        IMAGE_NAME = "biman82/springboot-demo"
        IMAGE_TAG = "1.0.${BUILD_NUMBER}"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Jar') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t %IMAGE_NAME%:%IMAGE_TAG% ."
            }
        }

        stage('Push Docker Image') {
            steps {
                bat "docker push %IMAGE_NAME%:%IMAGE_TAG%"
            }
        }
    }

    post {

        always {
            echo 'Pipeline execution completed.'
        }

        success {
            echo 'Pipeline executed successfully.'
            echo "Image Pushed: ${IMAGE_NAME}:${IMAGE_TAG}"
        }

        failure {
            echo 'Pipeline execution failed.'
        }

        cleanup {
            echo 'Cleanup completed.'
        }
    }
}