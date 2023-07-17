#!/usr/bin/env groovy

@Library('jenkins-shared-library')_

pipeline {

    agent any
    tools {
        maven 'Maven'
    }
    environment {
        IMAGE_NAME = 'chinmayapradhan/my-webapp:1.0'
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
                    def dockerCmd = "docker run -d -p 8090:8080 ${IMAGE_NAME}"
                    sshagent(['ec2-server-key']) {
                        sh "ssh -i -o StrictHostKeyChecking=no ec2-user@13.58.39.133 '${dockerCmd}'"
                    }
                }
            }
        }
    }
}
