#!/usr/bin/env groovy

@Library('jenkins-shared-library')_

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
                    buildWar()
                }
            }
        }
        stage('test') {
            steps {
                script {
                    echo "testing the appliation..."
                    buildImage('chinmayapradhan/my-webapp:1.0')
                    dockerLogin()
                    docker('chinmayapradhan/my-webapp:1.0')
                }
            }
        }
        stage('deploy') {
            steps {
                script {
                    echo "deployinging the appliation..."
                }
            }
        }
    }
}