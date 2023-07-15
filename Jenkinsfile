#!/usr/bin/env groovy

@Library('jenkins_shared_library')

def gv

pipeline {

    agent any
    tools {
        maven 'Maven'
    }

    stages {
        stage("increment version") {
            steps {
                script {
                    echo "incrementing the app version..."
                    sh 'mvn build-helper:parse-version versions:set \
                        -DnewVersion=\\\${parsedVersion.majorVersion}.\\\${parsedVersion.minorVersion}.\\\${nextIncrementalVersion} \
                        versions:commit'
                    def matcher = readFile('pom.xml') =~ '<version>(.+)</version>'
                    def version = matcher[0][1]
                    env.IMAGE_NAME = "$version-$BUILD_NUMBER"
                }
            }
        }
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
                    buildImage "chinmayapradhan/my-webapp:${IMAGE_NAME}"
                    dockerLogin()
                    dockerPush "chinmayapradhan/my-webapp:${IMAGE_NAME}"
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