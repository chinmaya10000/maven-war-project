#!/usr/bin/env groovy

library identifier: 'jenkins-shared-library@master', retriever: modernSCM(
        [$class: 'GitSCMSource',
         remote: 'https://github.com/chinmaya10000/jenkins-shared-library.git'
         credentialsId: 'git-hub-credentials'
        ]
)

def gv

pipeline {

    agent any
    tools {
        maven 'Maven'
    }

    stages {
        stage("init") {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }
        stage("build war") {
            steps {
                script {
                    buildWar()
                }
            }
        }
        stage("build and push image") {
            steps {
                script {
                    buildImage 'chinmayapradhan/my-webapp:3.0'
                    dockerLogin()
                    dockerPush 'chinmayapradhan/my-webapp:3.0'
                }
            }
        }
        stage("deploy") {
            steps {
                script {
                    gv.deployApp()
                }
            }
        }
    }
}