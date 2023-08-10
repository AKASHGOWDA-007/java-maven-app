#!/usr/bin/env groovy

library identifier: 'jenkins-shared-library@master', retriever: modernSCM(
    [$class: 'GitSCMSource',
    remote: 'https://github.com/AKASHGOWDA-007/jenkins-shared-library.git',
    credentialsID: 'github-credentials'
    ]
)
def gv

pipeline {
    agent any
    tools {
        maven "Maven"
    }
    stages {
        stage("init") {
            steps {
                script {
                    gv = load "script.groovy"
                    sh "Testing the integration of web hook with jenkins"
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
                    buildImage "akash712/my-repo:jma-3.0"
                    dockerLogin()
                    dockerPush "akash712/my-repo:jma-3.0"
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
