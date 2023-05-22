pipeline {
    agent any
    parameters {
        choice(name: 'ENV', choices: ['dev','prod'], description: 'chose the environment') 
       
    }
    options {
        ansiColor('xterm')  // ADD'S COLOUR TO THE OUTPUT : ENSURE YOU INSTALL ANSICOLOR PLUGIN
    }
    stages {
        stage('Backend') {
        parallel {
        stage('Destroy Cart') {
            steps {
            dir('cart')  { git branch: 'main', url: 'https://github.com/devops-anilkumar/cart.git' }
            sh '''
                 cd mutable-infra
                 terrafile -f env-${ENV}/Terrafile
                 terraform init -reconfigure -backend-config=env-${ENV}/${ENV}-backend.tfvars
                 terraform destroy -auto-approve -var-file=env-${ENV}/${ENV}.tfvars -var APP_VERSION=0.0.1
              '''
            }
        }
        stage('Destroy Catalogue') {
            steps {
            dir('catalogue') { git branch: 'main', url: 'https://github.com/devops-anilkumar/catalogue.git' }
              sh '''
                cd mutable-infra
                terrafile -f env-${ENV}/Terrafile
                terraform init -reconfigure -backend-config=env-${ENV}/${ENV}-backend.tfvars
                terraform destroy -auto-approve -var-file=env-${ENV}/${ENV}.tfvars -var APP_VERSION=0.0.1
              '''
            }
        }
        stage('Destroy User') {
            steps {
            dir('user') { git branch: 'main', url: 'https://github.com/devops-anilkumar/user.git' }
              sh '''
              cd mutable-infra
              terrafile -f env-${ENV}/Terrafile
              terraform init -reconfigure -backend-config=env-${ENV}/${ENV}-backend.tfvars
              terraform destroy -auto-approve -var-file=env-${ENV}/${ENV}.tfvars -var APP_VERSION=0.0.1
              '''
            }
        }
        stage('Destroy Shipping') {
            steps {
            dir('shipping') { git branch: 'main', url: 'https://github.com/devops-anilkumar/shipping.git' }
              sh '''
              cd mutable-infra
              terrafile -f env-${ENV}/Terrafile
              terraform init -reconfigure -backend-config=env-${ENV}/${ENV}-backend.tfvars
              terraform destroy -auto-approve -var-file=env-${ENV}/${ENV}.tfvars -var APP_VERSION=0.0.1
              '''
            }
        }
        stage('Destroy Payment') {
            steps {
            dir('payment') { git branch: 'main', url: 'https://github.com/devops-anilkumar/payment.git' }
              sh '''
              cd mutable-infra
              terrafile -f env-${ENV}/Terrafile
              terraform init -reconfigure -backend-config=env-${ENV}/${ENV}-backend.tfvars
              terraform destroy -auto-approve -var-file=env-${ENV}/${ENV}.tfvars -var APP_VERSION=0.0.1
              '''
            }
        }
        stage('Destroy Frontend') {
            steps {
            dir('frontend') { git branch: 'main', url: 'https://github.com/devops-anilkumar/frontend.git' }
              sh '''
              cd mutable-infra
              terrafile -f env-${ENV}/Terrafile
              terraform init -reconfigure -backend-config=env-${ENV}/${ENV}-backend.tfvars 
              terraform destroy -auto-approve -var-file=env-${ENV}/${ENV}.tfvars -var APP_VERSION=0.0.1
              '''
            }
        }
    }
}
        stage('Terraform Destroy Databases') {
            steps {
                git branch: 'main', url: 'https://github.com/devops-anilkumar/terraform-databases.git'
              sh "terrafile -f env-${ENV}/Terrafile"
              sh "terraform init -reconfigure -backend-config=env-${ENV}/${ENV}-backend.tfvars"
              sh "terraform plan -var-file=env-${ENV}/${ENV}.tfvars"
              sh "terraform destroy -auto-approve -var-file=env-${ENV}/${ENV}.tfvars"
            }
        }
        stage('Terraform Destroy ALB') {
            steps {
                git branch: 'main', url: 'https://github.com/devops-anilkumar/terraform-loadbalancers.git'
              sh "terrafile -f env-${ENV}/Terrafile"
              sh "terraform init -reconfigure -backend-config=env-${ENV}/${ENV}-backend.tfvars"
              sh "terraform plan -var-file=env-${ENV}/${ENV}.tfvars"
              sh "terraform destroy -auto-approve -var-file=env-${ENV}/${ENV}.tfvars"
            }
        }
        stage('Terraform Destroy Network') {
            steps {
                git branch: 'main', url: 'https://github.com/devops-anilkumar/terraform-vpc.git'
              sh "terrafile -f env-${ENV}/Terrafile"
              sh "terraform init -reconfigure -backend-config=env-${ENV}/${ENV}-backend.tfvars"
              sh "terraform plan -var-file=env-${ENV}/${ENV}.tfvars"
              sh "terraform destroy -auto-approve -var-file=env-${ENV}/${ENV}.tfvars"
            }
        }
    }
}