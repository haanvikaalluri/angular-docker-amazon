pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
    stages {
         stage('Clone repository') { 
            steps { 
                script{
                checkout scm
                }
            }
        }

        stage('Build') { 
            steps { 
                script{
                 app = docker.build("263187097115.dkr.ecr.us-east-1.amazonaws.com/ecr")
                }
            }
        }
        stage('Test'){
            steps {
                 echo 'Empty'
            }
        }
        stage('Deploy') {
            steps {
                script{
                       docker.withRegistry("https://263187097115.dkr.ecr.us-east-1.amazonaws.com/ecr", "ecr:us-east-1:857e99fc-f51e-4c8a-bf6a-bb1d1399f005") {
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                    }
                }
            }
        }
    }
}
