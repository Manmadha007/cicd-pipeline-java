pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Job 1
                echo 'Checking out code...'
                // Checkout code from your GitHub repository, specifying the branch
                git branch: 'TEST', url: 'https://github.com/Manmadha007/cicd-pipeline-java.git'
            }
        }
        stage('Build Job 1') {
            agent any  // Use the master/controller node
            steps {
                echo 'Building Job 1 on Built-In Node...'
                sh 'mvn clean compile'
            }
        }
        stage('Test Job 1') {
            agent any  // Use the master/controller node
            steps {
                echo 'Testing Job 1 on Built-In Node...'
                sh 'mvn test'
            }
        }
        stage('Deploy Job 1') {
            agent any  // Use the master/controller node
            steps {
                echo 'Deploying Job 1 on Built-In Node...'
                sh 'echo Deploying Job 1'
            }
        }
        stage('Build Job 2 on slave1') {
            agent { label 'slave1' }
            steps {
                echo 'Building Job 2 on slave1...'
                sh 'mvn clean compile'
            }
        }
        stage('Test Job 2 on slave1') {
            agent { label 'slave1' }
            steps {
                echo 'Testing Job 2 on slave1...'
                sh 'mvn test'
            }
        }
        stage('Deploy Job 2 on slave1') {
            agent { label 'slave1
