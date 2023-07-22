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
        stage('code review') {
            steps {
                script {
                    withSonarQubeEnv(credentialsId: 'sonar-qube-token') {
                        sh "sonar:sonar"
                    }
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