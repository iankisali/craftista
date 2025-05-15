pipeline {
  agent any
  stages {
    stage('Voting Build Stage') {
      steps {
        echo 'Compiling voting app...'
        dir(path: 'voting') {
          sh 'mvn compile'
        }

      }
    }

    stage('Voting Test Stage') {
      steps {
        dir(path: 'voting') {
          sh 'mvn clean test'
        }

      }
    }

    stage('Voting Package Stage') {
      steps {
        dir(path: 'voting') {
          sh 'mvn package -DskipTests'
        }

        archiveArtifacts '**/target/*.jar'
      }
    }

  }
  tools {
    maven 'Maven 3.9.9'
  }
  post {
    always {
      echo 'Pipeline completed..'
    }

  }
}