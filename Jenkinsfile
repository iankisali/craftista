pipeline {
  agent none
  stages {
    stage('Voting Build') {
      agent {
        docker {
          image 'maven:3.9.9-eclipse-temurin-17-alpine'
        }

      }
      steps {
        echo 'Compiling the voting application..'
        dir(path: 'voting') {
          sh 'mvn compile'
        }

      }
    }

    stage('Test Job') {
      agent {
        docker {
          image 'maven:3.9.9-eclipse-temurin-17-alpine'
        }

      }
      steps {
        dir(path: 'voting') {
          sh 'mvn clean test'
        }

      }
    }

    stage('Voting Package') {
      parallel {
        stage('Voting Package') {
          agent {
            docker {
              image 'maven:3.9.9-eclipse-temurin-17-alpine'
            }

          }
          steps {
            dir(path: 'voting') {
              sh 'mvn package -DskipTests'
              archiveArtifacts '**/target/*.jar'
            }

          }
        }

        stage('Voting Image B&P') {
          agent any
          steps {
            script {
              docker.withRegistry('https://index.docker.io/v1/', 'dockerlogin') {
                def commitHash = env.GIT_COMMIT.take(7)
                def dockerImage = docker.build("iankisali/craftista-voting:${commitHash}", "./voting")
                dockerImage.push()
                dockerImage.push("latest")
                dockerImage.push("dev")
              }
            }

          }
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