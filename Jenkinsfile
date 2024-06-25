pipelines {
    agent any
    environment {
        ENV_URL = "google.com"    // environment variable (global variable)
    }
    stages {
        stage("first stage") {
            steps{
               sh echo "Hello world from stage 1"
               sh echo "${ENV_URL}"
            }
        }
        stage("second stage") {
            environment {
                ENV_URL = "env.com"    //stage level variable (local variable)
              }
            steps{
                sh echo "Hi this stage 2"
                sh echo "${ENV_URL}"
            }
        }
        stage("third stage") {
            steps{
                echo "welcome to stage 3"
            }
        }
    }
}