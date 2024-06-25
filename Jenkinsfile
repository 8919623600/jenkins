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
    //   parameters {
    //     string(name: 'COMPONENT', defaultValue: 'MongoDB', description: 'choose  the component')
    //     text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
    //     booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
    //     choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
    // }
     tools {
        maven 'mvn-398' 
    }
    stages {
        stage("first stage") {
            steps{
               sh "echo Hello world from stage 1"
               sh "echo ${ENV_URL}" 
               sh "env"
            //    sh "sleep 60"
               sh "mvn --version"
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