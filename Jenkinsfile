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

    stage('Test Job') {
      steps {
        dir(path: 'voting') {
          sh 'mvn clean test'
        }

      }
    }

    stage('Voting Package') {
      steps {
        dir(path: 'voting') {
          sh 'mvn package -DskipTests'
          archiveArtifacts '**/target/*.jar'
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