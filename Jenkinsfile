pipeline {
    agent any

    stages{
        
        stage ("Git Checkout"){
            steps {

                git branch: 'main', url: 'https://github.com/CaptainDemir/demo-app2.git'
            
            }

        }
        stage ("Unit Testing"){
            steps {

                sh "mvn test"
            
            }

        }
        stage("Integration Testing"){
            
             steps{


             sh " mvn verify -DskipUnitTests"

             }
        }

        stage("Maven Build"){
            steps{
             
             sh"mvn clean install"

            }
        }

        stage("Static Code Analysis"){
            
            
            steps{

                scripts { withSonarQubeEnv(credentialsId: 'sonar-api') {
            
            sh "mvn clean package sonar:sonar"    

            }
            
            }
               
           
            
            }

        }
        
 }


}

