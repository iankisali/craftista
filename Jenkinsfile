pipeline {
  agent any
  stages {
    stage('Voting Build') {
      steps {
        echo 'Compiling the voting application..'
        dir(path: 'voting') {
          sh 'mvn compile'
        }

      }
    }

  }
  tools {
    maven 'Maven 3.9.9'
  }
  post {
    always {
      echo 'completed the pipeline craftista'
    }

  }
}