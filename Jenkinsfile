
    stages {
        stage('build') {
            steps {
                script {
                    echo "building the appliation..."
                    sh "mvn clean package"
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