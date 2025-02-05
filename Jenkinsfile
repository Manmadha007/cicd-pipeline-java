pipeline {
    agent any
    tools {
        maven 'MAVEN'
    }
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
                sh 'echo "Building the project..."'
                sh 'mvn clean install package'
            }
        }

        stage('Deploy') {
            steps {
                // Run a shell command for deploying
                sshagent(['c8af6165-b8b4-4468-8193-e5077da0440b']) {
                    sh "scp -o StrictHostKeyChecking=no target/MyLab-0.0.1.war ubuntu@54.67.2.80:/opt/tomcat/webapps"
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed!'
        }
    }
}
