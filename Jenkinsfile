def gv

pipeline {
    agent any
    tools {
        maven "Maven"
    }
    // parameters {
    //     choice(name: "VERSION", choices: ["1.1.0", "1.2.0", "1.3.0"], description: "")
    //     booleanParam(name: "executeTests", defaultValue: true, description: "")
    // }
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
                    echo "building the application..."
                    sh "mvn package"
                }
            }
        }
        stage("build image") {
            steps {
                script {
                    echo "building the image"
                    withCredentials([usernamePassword(credentialsId: "docker-hub-repo", passwordVariable: "PASS", usernameVariable: "USER")]) {
                        sh "docker build -t akash712/my-repo:jma-2.0 ."
                        sh "echo $PASS | docker login -u $USER --password-stdin"
                        sh "docker push akash712/my-repo:jma-2.0"
                    }
                }
            }
        }
        stage("deploy") {
            steps {
                script {
                    echo "Deploying to ${ENV}"
                }
            }
        }
    }
}
