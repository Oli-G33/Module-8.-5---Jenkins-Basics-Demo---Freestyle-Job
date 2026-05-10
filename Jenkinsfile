#!/user/bin/env groovy

library identifier: 'jenkins-shared-library@master', retriever: modernSCM(
    [
        $class: 'GitSCMSource',
        remote: 'https://github.com/Oli-G33/Module-8.-14---Jenkins-Shared-Library.git',
        credentialsId: 'github-credentials'
    ])
    
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
        stage("build jar") {
            steps {
                script {
                   buildJar()

                }
            }
        }

        stage("build and push image") {
            steps {
                script {
                    buildImage 'oligee/demo-app-jenkins:3.0'
                    dockerLogin()
                    dockerPush 'oligee/demo-app-jenkins:3.0'
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
