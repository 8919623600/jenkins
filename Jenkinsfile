pipeline {
    agent any
    environment {
        ENV_URL = "google.com"    // environment variable (global variable)
        SSHCRED = credentials('SSHCRED')          // saved creds on jenkins fetches as env variable SSHCRED_USR and SSHCRED
    }
    options { 
        disableConcurrentBuilds()
        buildDiscarder(logRotator(numToKeepStr: '1'))
     }
    stages {
        stage("first stage") {
            steps{
               sh "echo Hello world from stage 1"
               sh "echo ${ENV_URL}" 
               sh "env"
            }
        }
        stage("second stage") {
            environment {
                ENV_URL = "env.com"    //stage level variable (local variable)
              }
            steps{
                sh "echo Hi this stage 2"
                sh "echo ${ENV_URL}"
            }
        }
        stage("third stage") {
            steps{
                echo "welcome to stage 3"
            }
        }
    }
}