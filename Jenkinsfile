pipeline {
  agent any

  tools {
    maven 'Maven 3.9.9'
  }
    stages{
      stage("Voting Build Stage"){
        steps{
          echo 'Compiling voting app...'
          dir ('voting'){
            sh 'mvn compile'
          }
        }
      }
    }
    
    post{
      always{
        echo 'Pipeline completed..'
      }
    }
}