pipeline {
    agent any  // Runs on any available agent
    stages {
        stage('Checkout Job 1 (Test branch)') {
            agent { label 'master' }  // Job 1 runs on master node
            steps {
                echo 'Checking out code from the test branch...'
                git branch: 'test', url: 'https://github.com/Manmadha007/cicd-pipeline-java.git'
            }
        }

        stage('Checkout Job 2 (Main branch)') {
            agent { label 'slave1' }  // Job 2 runs on slave1 node
            steps {
                echo 'Checking out code from the main branch...'
                git branch: 'main', url: 'https://github.com/Manmadha007/cicd-pipeline-java.git'
            }
        }

        stage('Build Job 1 (Test branch)') {
            agent { label 'master' }  // Build Job 1 on master node
            steps {
                echo 'Building Job 1 on master node...'
                sh 'mvn clean compile'
            }
        }

        stage('Build Job 2 (Main branch)') {
            agent { label 'slave1' }  // Build Job 2 on slave1 node
            steps {
                echo 'Building Job 2 on slave1 node...'
                sh 'mvn clean compile'
            }
        }

        stage('Test Job 1 (Test branch)') {
            agent { label 'master' }  // Test Job 1 on master node
            steps {
                echo 'Running tests for Job 1 (Test branch)...'
                sh 'mvn test'
            }
        }

        stage('Test Job 2 (Main branch)') {
            agent { label 'slave1' }  // Test Job 2 on slave1 node
            steps {
                echo 'Running tests for Job 2 (Main branch)...'
                sh 'mvn test'
            }
        }

        stage('Deploy Job 1 (Test branch)') {
            agent { label 'master' }  // Deploy Job 1 on master node
            steps {
                echo 'Deploying Job 1 (Test branch) on master node...'
                sh 'echo Deploying Job 1'
            }
        }

        stage('Deploy Job 2 (Main branch)') {
            agent { label 'slave1' }  // Deploy Job 2 on slave1 node
            steps {
                echo 'Deploying Job 2 (Main branch) on slave1 node...'
                sh 'echo Deploying Job 2'
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
