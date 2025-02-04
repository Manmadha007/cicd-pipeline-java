pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                // Replace with your SCM checkout command
                // For example, for Git:
                // git url: 'https://github.com/Manmadha007/cicd-pipeline-java.git'
            }
        }
        stage('Build') {
            steps {
                echo 'Building the application...'
                // Add your build commands here
                // For example, for a Maven project:
                // sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                // Add your test commands here
                // For example, for a Maven project:
                // sh 'mvn test'
            }
        }
    }
}
