// example of showing declearitive pipeline
pipeline {
    agent (label 'ws' )

        environment { 
           ENV_URL = "pipeline.learning.com"  // declaring varibles at pipeline level
           SSH_CREDENTIALS = credentials('SSH_CRED')
        }
   //      triggers { pollSCM('*/1 * * * *') }

   //      parameters {
   //      string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')

   //      text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')

   //      booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')

   //      choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')

   //      password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
   //  }

    tools {
        maven 'maven-3.8.6' 
    }

    stages {
      stage ('example on parallel stages'){
         parallel{
            stage ('one'){
               steps{
                  sh "ifconfig"
                  sh "echo stage one"
                  sh "sleep 6"
               }
            }
           stage ('two'){
               steps{
                  sh "echo stage two"
                  sh "sleep 6"
               }
            }
           stage ('three'){
               steps{
                  sh "echo stage three"
                  sh "sleep 6"
               }
            }
         }
      }
         stage ('testing mvn commands'){
         steps{
            sh "mvn  --version"
         }   
    }
         stage ('stage name - 1') {
            steps {
            sh "echo this is my first stage in the jenkins pipeline"
            }
         }
    
         stage ('stage name - 2') {
            when { branch 'dev' }
            steps {
            sh "echo printing the environment variable ${ENV_URL}"
            sh "env"
            }
         }
         stage ('final stage ; needs attention') {
           input {
                message "Should we continue?"
                ok "Yes, we should."
                submitter "alice,bob"
                parameters {
                    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                }
            }
                       environment { 
           ENV_URL = "stage.learning.com"  // declaring varibles at stage  level in pipeline 
        }
           steps {
                sh '''echo i am using pipeline syntax help
                      echo demo to show multiple lines
                      echo printing multiple lines with a single usage of sh command
                      echo printing the environment variable ${ENV_URL}
                    '''
            }
          }
    }
}