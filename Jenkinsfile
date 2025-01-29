pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Job 1
                echo 'Checking out code...'
                // Checkout code from your GitHub repository
                git branch: 'TEST', url: 'https://github.com/Manmadha007/cicd-pipeline-java.git'
            }
        }
        stage('Build Job 1') {
            agent { label 'master' } // Use the master/controller node
            steps {
                echo 'Building Job 1 on Built-In Node...'
                sh 'mvn clean compile'
            }
        }
        stage('Build Job 2 on slave1') {
            agent { label 'slave1' }  // Use the slave1 node for this stage
            steps {
                echo 'Building Job 2 on slave1...'
                sh 'mvn clean compile'
            }
        }
    }
    post {
        always {
            echo 'Cleaning up...'
            // Perform cleanup actions, e.g., deleting temporary files
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
}
