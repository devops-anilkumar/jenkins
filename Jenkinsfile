// example of showing declearitive pipeline
pipeline {
    agent any
    stages {
         
         stage ('stage name - 1') {
            steps {
            sh "echo this is my first stage in jenkins pipeline"
            }
         }
    
         stage ('stage name - 2') {
            steps {
            sh "echo i am excuting stage 2"
            }
         }
          stage ('stage name - 3') {
            steps {
                sh '''echo i am using pipeline syntax help
                      echo demo to show multiple lines
                      echo printing multiple lines with a single usage of sh
                    '''
            }
          }
    }
}