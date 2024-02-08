pipeline {
    agent any
    
    tools {
        maven 'My_Maven'
    }
    parameters {
         string(name: 'staging_server', defaultValue: '13.232.37.20', description: 'Remote Staging Server')
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

        stage ('Deployments'){
            parallel{
                stage ("Deploy to Staging"){
                    steps {
                        deploy adapters: [tomcat9(credentialsId: '90927b6b-514b-4644-8ad0-9e40d9533462', path: '', url: 'http://54.158.155.78:8081/')], contextPath: null, war: '**/*.war'
                    }
                }
            }
        }
    }
}
