pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
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