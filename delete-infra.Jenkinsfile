pipeline {
    agent { 
        label 'ws'                  // while creating the node we have given the label of node as ws. Job will run on node machine
        }
    environment {
        ENV = "dev" 
        AWS_ACCESS_KEY_ID = credentials('Access_key')
        AWS_SECRET_ACCESS_KEY = credentials('Secret_access_key')
    }
    options {
        // ansiColor('xterm')
        buildDiscarder(logRotator(numToKeepStr: '1')) 
        disableConcurrentBuilds()
        timeout(time: 35, unit: 'MINUTES')
    }
    // parameters {
    //     choice(name: 'ENV', choices: ['dev', 'prod'], description: 'Select the environment')
    // }
    
    stages {

        stage('Deleting EKS') {
            steps {
                dir('k8s') {
                git branch: 'main', url: 'https://github.com/8919623600/terraform-kubernetes.git'
                        sh '''
                            cd eks
                            make destroy
                        '''
                }
            }
        }
         
         stage('Deleting Databases') {
            steps {
                dir('DB') {
                git branch: 'main', url: 'https://github.com/8919623600/terraform-databases.git'
                        sh '''
                            terrafile -f env-dev/Terrafile
                            terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure
                            terraform destroy -auto-approve -var-file=env-${ENV}/${ENV}.tfvars -var ENV=${ENV}
                          '''
                }
            }
        }

        stage('Deleting VPC') {
            steps {
                dir('VPC') {
                git branch: 'main', url: 'https://github.com/8919623600/manu_terraform.git'
                        sh '''
                            cd terraform-vpc/
                            terrafile -f env-dev/Terrafile
                            terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure
                            terraform destroy -auto-approve -var-file=env-${ENV}/${ENV}.tfvars -var ENV=${ENV}
                        '''
                }
            }
        }
       
    }
}

