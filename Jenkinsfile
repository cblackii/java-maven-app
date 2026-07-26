#!/usr/bin/env groovy

library(
    identifier: 'jenkins-shared-library@main',
    retriever: modernSCM([
        $class: 'GitSCMSource',
        remote: 'https://github.com/cblackii/java-maven-app.git',
        credentialsId: 'github-credentials'
    ])
)

def gv

pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {
        stage('Init') {
            steps {
                script {
                    gv = load 'script.groovy'
                }
            }
        }

        stage('Build JAR') {
            steps {
                script {
                    gv.buildJar()
                }
            }
        }

        stage('Build Image') {
            steps {
                script {
                    gv.buildImage()
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    gv.deployApp()
                }
            }
        }
    }
}
