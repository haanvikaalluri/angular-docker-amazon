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
                 app = docker.build("263187097115.dkr.ecr.us-east-1.amazonaws.com/aws-docker-demo")
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
                       docker.withRegistry("https://263187097115.dkr.ecr.us-east-1.amazonaws.com/aws-docker-demo", "ecr:us-east-1:AKIAT2RZMMYNVUMBAUJV") {
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                    }
                }
            }
        }
    }
}
