pipeline {

    agent any

    stages {
        stage('test') {
            steps {
                script {
                    echo "testing the appliation..."
                    echo "Executing the pipeline for branch $BRANCH_NAME"
                }
            }
        }
        stage('build') {
            when {
                expression {
                    BRANCH_NAME == 'master'
                }
            }
            steps {
                script {
                    echo "building the appliation..."
                }
            }
        }
        stage('deploy') {
            when {
                expression {
                    BRANCH_NAME == 'master'
                }
            }
            steps {
                script {
                    echo "deployinging the appliation..."
                }
            }
        }
    }
}