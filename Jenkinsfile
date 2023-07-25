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
                    def nexusServer = 'nexus-repo' // The ID of the Nexus server credentials in Jenkins
                    def nexusUrl = 'https://18.189.186.218:8081/' // URL of your Nexus repository
                    def mavenArtifact = 'target/*.war' // The path to the artifact you want to upload

                    nexusArtifactUploader(credentialsId: nexusServer, nexusUrl: nexusUrl, groupId: 'com.cloudbots.www', version: '1.0-SNAPSHOT', repository: 'warproj-snapshot-repository', file: mavenArtifact)
                }
            }
        }
        stage('deploy') {
            steps {
                script {
                    echo "deploying the application.."
                }
            }
        }
    }
}