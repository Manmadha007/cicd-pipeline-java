pipeline {
    agent none  // No global agent, we define agents for each stage

    tools {
        maven 'maven'
    }

    environment {
        ArtifactId = readMavenPom().getArtifactId()
        Version = readMavenPom().getVersion()
        GroupId = readMavenPom().getGroupId()
        Name = readMavenPom().getName()
    }

    stages {
        // Stage for jobs that will run on the master
        stage('Build on Master - Job 1') {
            agent { label 'master' }
            steps {
                sh 'mvn clean install package'
            }
        }

        stage('Test on Master - Job 2') {
            agent { label 'master' }
            steps {
                echo 'Testing on Master...'
            }
        }

        stage('Publish to Nexus on Master - Job 3') {
            agent { label 'master' }
            steps { 
                script {
                    def NexusRepo = Version.endsWith("SNAPSHOT") ? "MyLab-SNAPSHOT" : "MyLab-RELEASE"
                    
                    nexusArtifactUploader artifacts: 
                    [
                        [
                            artifactId: "${ArtifactId}", 
                            classifier: '', 
                            file: "target/${ArtifactId}-${Version}.war", 
                            type: 'war'
                        ]
                    ], 
                    credentialsId: 'nexus', 
                    groupId: "${GroupId}", 
                    nexusUrl: '10.0.0.167:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: "${NexusRepo}", 
                    version: "${Version}"
                }
            }
        }

        stage('Print Environment variables on Master - Job 4') {
            agent { label 'master' }
            steps {
                echo "Artifact ID is '${ArtifactId}'"
                echo "Group ID is '${GroupId}'"
                echo "Version is '${Version}'"
                echo "Name is '${Name}'"
            }
        }

        stage('Deploy to Docker on Master - Job 5') {
            agent { label 'master' }
            steps {
                echo 'Deploying on Master...'
                sshPublisher(publishers: 
                [sshPublisherDesc(
                    configName: 'ansible-controller', 
                    transfers: [
                        sshTransfer(
                            sourceFiles: 'download-deploy.yaml, hosts',
                            remoteDirectory: '/playbooks',
                            cleanRemote: false,
                            execCommand: 'cd playbooks/ && ansible-playbook download-deploy.yaml -i hosts', 
                            execTimeout: 120000, 
                        )
                    ], 
                    usePromotionTimestamp: false, 
                    useWorkspaceInPromotion: false, 
                    verbose: false)
                ])
            }
        }

        // Stage for jobs that will run on slave1
        stage('Build on Slave1 - Job 6') {
            agent { label 'slave1' }
            steps {
                sh 'mvn clean install package'
            }
        }

        stage('Test on Slave1 - Job 7') {
            agent { label 'slave1' }
            steps {
                echo 'Testing on Slave1...'
            }
        }

        stage('Publish to Nexus on Slave1 - Job 8') {
            agent { label 'slave1' }
            steps { 
                script {
                    def NexusRepo = Version.endsWith("SNAPSHOT") ? "MyLab-SNAPSHOT" : "MyLab-RELEASE"
                    
                    nexusArtifactUploader artifacts: 
                    [
                        [
                            artifactId: "${ArtifactId}", 
                            classifier: '', 
                            file: "target/${ArtifactId}-${Version}.war", 
                            type: 'war'
                        ]
                    ], 
                    credentialsId: 'nexus', 
                    groupId: "${GroupId}", 
                    nexusUrl: '10.0.0.167:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: "${NexusRepo}", 
                    version: "${Version}"
                }
            }
        }

        stage('Print Environment variables on Slave1 - Job 9') {
            agent { label 'slave1' }
            steps {
                echo "Artifact ID is '${ArtifactId}'"
                echo "Group ID is '${GroupId}'"
                echo "Version is '${Version}'"
                echo "Name is '${Name}'"
            }
        }

        stage('Deploy to Docker on Slave1 - Job 10') {
            agent { label 'slave1' }
            steps {
                echo 'Deploying on Slave1...'
                sshPublisher(publishers: 
                [sshPublisherDesc(
                    configName: 'ansible-controller', 
                    transfers: [
                        sshTransfer(
                            sourceFiles: 'download-deploy.yaml, hosts',
                            remoteDirectory: '/playbooks',
                            cleanRemote: false,
                            execCommand: 'cd playbooks/ && ansible-playbook download-deploy.yaml -i hosts', 
                            execTimeout: 120000, 
                        )
                    ], 
                    usePromotionTimestamp: false, 
                    useWorkspaceInPromotion: false, 
                    verbose: false)
                ])
            }
        }
    }
}
