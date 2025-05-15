pipeline {
  agent any
  stages {
    stage('Voting Build Stage') {
      agent {
        docker {
          image 'maven:3.9.9-eclipse-temurin-17-alpine'
        }

      }
      steps {
        echo 'Compiling voting app...'
        dir(path: 'voting') {
          sh 'mvn compile'
        }

      }
    }

    stage('Voting Test Stage') {
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

    stage('Voting Package Stage') {
      parallel {
        stage('Voting Package Stage') {
          agent {
            docker {
              image 'maven:3.9.9-eclipse-temurin-17-alpine'
            }

          }
          steps {
            dir(path: 'voting') {
              sh 'mvn package -DskipTests'
            }

            archiveArtifacts '**/target/*.jar'
          }
        }

        stage('Voting Build and Package Image') {
          agent any
          steps {
            script {
              docker.withRegistry('https://index.docker.io/v1/', '1a345b27-4422-4d9e-a238-a2b2d854faa5') {
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
      echo 'Pipeline completed..'
    }

  }
}