pipeline {
    agent any
    
    tools {
        maven 'My_Maven'
    }
    

    stages{
       stage('Build'){
          steps {
               sh 'mvn clean package'
          }
          post {
               success {
                   echo 'Archiving the artifacts'
                   archiveArtifacts artifacts: '**/target/*.war'
               }
          }
       }

    }
}
