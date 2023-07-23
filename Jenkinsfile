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
                        sh "sonar-scanner"
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