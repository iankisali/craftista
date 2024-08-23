pipeline {
    agent any
    tools {
        Maven 'Maven 3.9.9'
    }
        stages {
            stage("Voting Build") {
                steps {
                    echo 'Compiling the voting application..'
                    dir('voting') {
                        sh 'mvn compile'
                    }
                }
            }


            // stage("") {
            //     steps {
                    
            //     }
            // }
        }
    post {
        always {
            echo 'completed the pipeline craftista'
        }
    }
}