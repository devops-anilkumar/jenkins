pipeline {
    agent any
    parameters {
        choice(name: 'ENV', choices: ['dev','prod'], description: 'chose the environment') 
       
    }
    options {
        ansiColor('xterm')  // ADD'S COLOUR TO THE OUTPUT : ENSURE YOU INSTALL ANSICOLOR PLUGIN
    }
    stages {
        stage('Terraform Destroy Network') {
            steps {
                gitbranch: 'main', url: 'https://github.com/devops-anilkumar/terraform-vpc.git'
              sh "terrafile -f env-${ENV}/Terrafile"
              sh "terraform init -backend-config=env-${ENV}/${ENV}-backend.tfvars"
              sh "terraform plan -var-file=env-${ENV}/${ENV}.tfvars"
              sh "terraform destroy -auto-approve -var-file=env-${ENV}/${ENV}.tfvars"
            }
        }
        stage('Terraform Destroy Databases') {
            steps {
                gitbranch: 'main', url: 'https://github.com/devops-anilkumar/terraform-databases.git'
              sh "terrafile -f env-${ENV}/Terrafile"
              sh "terraform init -backend-config=env-${ENV}/${ENV}-backend.tfvars"
              sh "terraform plan -var-file=env-${ENV}/${ENV}.tfvars"
              sh "terraform destroy -auto-approve -var-file=env-${ENV}/${ENV}.tfvars"
            }
        }
    }
}