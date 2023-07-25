pipeline {
    
    agent any 
    tools {
        maven 'Maven'
    }
    
    
    stages {
        stage('build') {
            steps {
                script {
                    echo "building the appliation..."
                    sh "mvn clean package"
                }
            }
        }
        stage('SonarQube Analysis') {
            steps {
                script {
                    echo "Run SonarQube Scanner to analyze the code.."
                    withSonarQubeEnv('Sonar-Server-10.1') {
                        sh "mvn sonar:sonar"
                    }
                }
            }
        }
        stage('Nexus Repository Upload') {
            steps {
                script {
                    nexusArtifactUploader artifacts: [[artifactId: 'cloudbots_warproj', classifier: '', file: 'target/cloudbots_warproj.war', type: 'war']], credentialsId: 'nexus-repo', groupId: 'com.cloudbots.www', nexusUrl: '18.189.186.218:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'warproj-snapshot-repository', version: '1.0-SNAPSHOT'
                }
            }
        }
        stage('deploy') {
            steps {
                script {
                    echo "deploying the application.."
                    sshagent(['ec2-server-key']) {
                        sh "scp -o StrictHostKeyChecking=no target/cloudbots_warproj.war ec2-user@3.12.147.158:/opt/tomcat/webapps"
                    }
                }
            }
        }
    }
}