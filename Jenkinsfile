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
                 app = docker.build("263187097115.dkr.ecr.us-east-1.amazonaws.com/angular-docker-amzon-ecs")
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
                       
                    withDockerRegistry(credentialsId: 'ecr:us-east-1:AKIAT2RZMMYNZKNOUVOS', url: 'https://263187097115.dkr.ecr.us-east-1.amazonaws.com/angular-docker-amzon-ecs') {
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                    }
                }
            }
        }
    }
}
