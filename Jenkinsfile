pipeline {
    agent any
    environment {
        ENV_URL = "google.com"    // environment variable (global variable)
        SSHCRED = credentials('SSHCRED')          // saved creds on jenkins fetches as env variable SSHCRED_USR and SSHCRED
    }
    options { 
        disableConcurrentBuilds()                         // parrallely builds dont run
        buildDiscarder(logRotator(numToKeepStr: '1'))     // controlling log rotation
        timeout(time: 5, unit: 'MINUTES')                 // if the job is taking more than 5 minute then it will get killed
     }
    stages {
        stage("first stage") {
            steps{
               sh "echo Hello world from stage 1"
               sh "echo ${ENV_URL}" 
               sh "env"
            //    sh "sleep 60"
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