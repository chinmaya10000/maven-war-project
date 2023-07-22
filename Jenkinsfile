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
                    withSonarQubeEnv(sonar-server-10.1) {
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