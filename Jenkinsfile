pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Clone the GitHub repository
               git branch: 'tomcat', url: 'https://github.com/Manmadha007/cicd-pipeline-java.git'
            }
        }

        stage('Build') {
            steps {
                // Run a shell command (e.g., build or compile)
                sh 'echo "Building the project..."'
            }
        }

        stage('Test') {
            steps {
                // Run a shell command for testing
                sh 'echo "Running tests..."'
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed!'
        }
    }
}
