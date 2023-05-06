pipeline {
    agent any
    parameters {
        choice(name: 'ENV', choices: ['dev','prod'], description: 'chose the environment') 
       
    }
    options {
        ansiColor('xterm')  // ADD'S COLOUR TO THE OUTPUT : ENSURE YOU INSTALL ANSICOLOR PLUGIN
    }
    stages {
        stage('Terraform Create Network') {
            steps {
                gitbranch: 'main', url: 'https://github.com/devops-anilkumar/terraform-vpc.git'
              sh "terrafile -f env-${ENV}/Terrafile"
              sh "terraform init -backend-config=env-${ENV}/${ENV}-backend.tfvars"
              sh "terraform plan -var-file=env-${ENV}/${ENV}.tfvars"
              sh "terraform apply -auto-approve -var-file=env-${ENV}/${ENV}.tfvars"
            }
        }
        stage('Terraform Create Databases') {
            steps {
                gitbranch: 'main', url: 'https://github.com/devops-anilkumar/terraform-databases.git'
              sh "terrafile -f env-${ENV}/Terrafile"
              sh "terraform init -backend-config=env-${ENV}/${ENV}-backend.tfvars"
              sh "terraform plan -var-file=env-${ENV}/${ENV}.tfvars"
              sh "terraform apply -auto-approve -var-file=env-${ENV}/${ENV}.tfvars"
            }
        }
    }
}