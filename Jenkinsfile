pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code...'
                git branch: 'TEST', url: 'https://github.com/Manmadha007/cicd-pipeline-java.git'
            }
        }
        stage('Build Job 1') {
            agent { label 'master' }  // Explicitly use the master node for this stage
            steps {
                echo 'Building Job 1 on Built-In Node...'
                sh 'mvn clean compile'
            }
        }
    }
    post {
        always {
            echo 'Cleaning up...'
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
}
