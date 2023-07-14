#!/usr/bin/env groovy

@Library('jenkins-shared-library')
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
        stage("build image") {
            steps {
                script {
                    buildImage 'chinmayapradhan/my-webapp:3.0'
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