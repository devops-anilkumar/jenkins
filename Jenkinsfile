// example of showing declearitive pipeline
pipeline {
    agent any

        environment { 
           ENV_URL = "pipeline.learning.com"  // declaring varibles at pipeline level
        }


    stages {
         
         stage ('stage name - 1') {
            steps {
            sh "echo this is my first stage in jenkins pipeline"
            }
         }
    
         stage ('stage name - 2') {
            steps {
            sh "echo printing the environment variable ${ENV_URL}"
            }
         }
          stage ('stage name - 3') {
            steps {
                       environment { 
           ENV_URL = "stage.learning.com"  // declaring varibles at stage  level in pipeline 
        }
                sh '''echo i am using pipeline syntax help
                      echo demo to show multiple lines
                      echo printing multiple lines with a single usage of sh command
                      echo printing the environment variable ${ENV_URL}
                    '''
            }
          }
    }
}