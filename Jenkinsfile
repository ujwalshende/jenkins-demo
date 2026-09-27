#!user/bin/env groovy
library identifier: 'jenkins-shared-library@master', retriever: modernSCM(
    [$class: 'GitSCMSource',
    remote: 'https://github.com/ujwalshende/jenkins-shared-library.git',
    credentialsId: 'github-password' ]
)

def gv

pipeline{
    agent any
    tools{
        maven 'maven-3.9.16'
    }
    stages {
        stage("init"){
            steps{
                script{
                    gv =  load "script.groovy"
                }
            }
        }
        stage("build jar") {
            steps{
                script{
                    buildJar()

                }
            }
        }
        stage("build and push image") {
            steps{
                script{
                    buildImage 'uds10/demo-app:jma-3.0'
                    dockerLogin()
                    dockerPush 'uds10/demo-app:jma-3.0'
                }

            }
        }
        stage("deploy"){
            steps{
                script{
                    gv.deployApp()
                }
            }
        }
    }
}