// example of showing declearitive pipeline
pipeline {
    agent any

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


    stages {
         stage ('testing mvn commands'){
         steps{
            sh "mvn  clean"
         }   
    }
         stage ('stage name - 1') {
            steps {
            sh "echo this is my first stage in the jenkins pipeline"
            }
         }
    
         stage ('stage name - 2') {
            steps {
            sh "echo printing the environment variable ${ENV_URL}"
            sh "env"
            }
         }
          stage ('stage name - 3') {
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