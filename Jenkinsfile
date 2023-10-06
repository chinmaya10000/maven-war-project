pipeline {

    agent any 
    stages {
        stage("copy files to ansible server") {
            steps {
                script {
                    echo "copying all neccessary files to ansible control node"
                    sshagent(['ansible-server-key']) {
                        sh "scp -o StrictHostKeyChecking=no ansible/* ubuntu@13.59.21.14:/home/ubuntu"

                        withCredentials([sshUserPrivateKey(credentialsId: 'ec2-server-key', keyFileVariable: 'keyfile', usernameVariable: 'USER')]) {
                            sh 'scp $keyfile ubuntu@13.59.21.14:/home/ubuntu/ssh-key.pem'
                        }
                    }
                }
            }
        }
    }
}