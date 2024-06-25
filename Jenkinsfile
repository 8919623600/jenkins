pipeline {
    agent { 
        label 'ws'                  // while creating the node we have given the label of node as ws. Job will run on node machine
        }

    environment {
        ENV_URL = "google.com"    // environment variable (global variable)
        SSHCRED = credentials('SSHCRED')          // saved creds on jenkins fetches as env variable SSHCRED_USR and SSHCRED
    }

    options { 
        disableConcurrentBuilds()                         // parrallely builds dont run
        buildDiscarder(logRotator(numToKeepStr: '1'))     // controlling log rotation
        timeout(time: 5, unit: 'MINUTES')                 // if the job is taking more than 5 minute then it will get killed
     } 
    // triggers{ cron('H/15 * * * *') }                  // it will run the build at given time whether changes are there or not
    // triggers{ pollSCM('H/15 * * * *') }               // it will run the build at given time if there is any changes in the code

    parameters {
        string(name: 'COMPONENT', defaultValue: 'MongoDB', description: 'choose  the component')
        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
    }

     tools {
        maven 'mvn-398'        // this tool is defined in pipeline level which will serve for all stages
    }
    stages {
        stage("first stage") {
            steps{
               sh "echo Hello world from stage 1"
               sh "echo ${ENV_URL}" 
               sh "env"
            //    sh "sleep 60"
               sh "mvn --version"
               sh "hostname"
            }
        }
        stage("second stage") {
            environment {
                ENV_URL = "env.com"    //stage level variable (local variable)
              }
            tools {
               maven 'mvn-384' 
             }
            steps{
                sh "echo Hi this stage 2"
                sh "echo ${ENV_URL}"
                sh "mvn --version"        // maven installed for this specific stage
            }
        }
        stage("third stage") {
            steps{
                echo "welcome to stage 3"
            }
        }
        stage ("tesing stages")  {
            parallel {                               // under parallel block there are 3 stages which will run parallely
                stage ("unit testing") {
                 steps {
                    sh "echo unit testing in progress"
                    sh "sleep 30"
                 }
            }
               stage ("integration testing") {
                 steps {
                    sh "echo integration testing in progress"
                    sh "sleep 30"
                 }
         }
              stage ("functional testing") {
                 steps {
                    sh "echo functional testing in progress"
                    sh "sleep 30"
                 }
         }
     }
  }
}
}