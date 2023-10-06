pipeline {

    agent any 
    stages {
        stage("copy files to ansible server") {
            steps {
                script {
                    echo "copying all neccessary files to ansible control node"
                    sshagent(['ansible-server-key']) {
                        sh "scp -o StrictHostKeyChecking=no ansible/* ubuntu@3.14.70.59:/home/ubuntu"

                        withCredentials([sshUserPrivateKey(credentialsId: 'ec2-server-key', keyFileVarible: 'keyfile', usernameVariable: 'USER')]) {
                            sh 'scp $keyfile ubuntu@3.14.70.59:/home/ubuntu/ssh-key.pem'
                        }
                    }
                }
            }
        }
    }
}