pipeline {

    agent { docker { image 'maven:3.6.3' }}
//     agent any
    stages {

        stage('Build') {
            steps {
                sh 'mvn --version'
                echo 'Build'
            }
        }

        stage('Integration Test') {
            steps {
                echo 'Test'
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }

        success {
            echo 'Pipeline executed successfully.'
        }

        failure {
            echo 'Pipeline execution failed.'
        }

        unstable {
            echo 'Pipeline is unstable.'
        }

        changed {
            echo 'Pipeline result changed from the previous build.'
        }

        cleanup {
            echo 'Performing cleanup...'
        }
    }
}