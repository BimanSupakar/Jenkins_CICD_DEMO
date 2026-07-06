pipeline {

    agent any

    environment {
        IMAGE_NAME = "bimansupakar/springboot-demo"
        IMAGE_TAG = "${BUILD_NUMBER}"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Jar') {
            steps {
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME%:%IMAGE_TAG% .'
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
                        credentialsId: 'dockerhub',
                        usernameVariable: 'DOCKER_USERNAME',
                        passwordVariable: 'DOCKER_PASSWORD'
                )]) {

                    bat 'echo %DOCKER_PASSWORD% | docker login -u %DOCKER_USERNAME% --password-stdin'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                bat 'docker push %IMAGE_NAME%:%IMAGE_TAG%'
            }
        }

    }

    post {

        always {
            echo 'Pipeline execution completed.'
        }

        success {
            echo 'Docker image pushed successfully.'
        }

        failure {
            echo 'Pipeline execution failed.'
        }

        cleanup {
            bat 'docker logout'
            echo 'Cleanup completed.'
        }

    }
}