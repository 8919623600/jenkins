pipeline {
    agent { 
        label 'ws'                  // while creating the node we have given the label of node as ws. Job will run on node machine
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
        stage('Creating VPC') {
            steps {
                dir('VPC') {
                git branch: 'main', url: 'https://github.com/8919623600/manu_terraform.git'
                        sh '''
                            cd terraform-vpc/
                            rm -rf .terraform
                            terrafile -f env-dev/Terrafile
                            terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure
                            terraform plan -var-file=env-${ENV}/${ENV}.tfvars -var ENV=${ENV}
                            terraform apply -auto-approve -var-file=env-${ENV}/${ENV}.tfvars -var ENV=${ENV}
                        '''
                }
            }
        }


        // stage('Creating EKS') {
        //     steps {
        //         dir('k8s') {
        //         git branch: 'main', url: 'https://github.com/b57-clouddevops/kubernetes.git'
        //                 sh '''
        //                     cd eks
        //                     make create
        //                 '''
        //         }
        //     }
        // }
        stage('Creating Databases') {
            steps {
                dir('DB') {
                git branch: 'main', url: 'https://github.com/8919623600/manu_terraform.git'
                        sh '''
                            cd terraform-databases/
                            rm -rf .terraform
                            terrafile -f env-dev/Terrafile
                            terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure
                            terraform plan -var-file=env-${ENV}/${ENV}.tfvars -var ENV=${ENV}
                            terraform apply -auto-approve -var-file=env-${ENV}/${ENV}.tfvars -var ENV=${ENV}
                        '''
                }
            }
        }
    }
}