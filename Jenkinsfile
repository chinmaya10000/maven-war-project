#!/usr/bin/env groovy

@Library('jenkins-shared-library')_

pipeline {

    agent any
    tools {
        maven 'Maven'
    }
    environment {
        IMAGE_NAME = 'chinmayapradhan/my-webapp:2.0'
    }

    stages {
        stage('build app') {
            steps {
                script {
                    echo "building the appliation..."
                    buildWar()
                }
            }
        }
        stage('build image') {
            steps {
                script {
                    echo "building docker image..."
                    buildImage(env.IMAGE_NAME)
                    dockerLogin()
                    dockerPush(env.IMAGE_NAME)
                }
            }
        }
        stage('deploy') {
            steps {
                script {
                    echo "deployinging the appliation..."

                    def shellCmd = "bash ./server-cmds.sh"
                    def ec2Instance = "ec2-user@18.223.125.125"
                    sshagent(['ec2-server-key']) {
                        sh "scp server-cmds.sh ${ec2Instance}:/home/ec2-user"
                        sh "scp docker-compose.yml ${ec2Instance}:/home/ec2-user"
                        sh "ssh -o StrictHostKeyChecking=no ${ec2Instance} '${shellCmd}'"
                    }
                }
            }
        }
    }
}
