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
                
                script{
                    
                    withSonarQubeEnv(credentialsId: 'sonar-api') {
                        
                        sh 'mvn clean package sonar:sonar'
                    }
                   }
                    
                }

        }


        stage('Quality Gate Status'){

            steps{

                script{

                     waitForQualityGate abortPipeline: false, credentialsId: 'sonar-api'

                }
            }
        }


        stage("uploda war file to nexu"){

            steps{

                script{

                    nexusArtifactUploader artifacts: 
                    [
                        [
                            artifactId: 'springboot', classifier: '', file: 'target/Uber.jar', type: 'jar'
                            ]
                    ], 
                    credentialsId: '', 
                    groupId: 'com.example', 
                    nexusUrl: '127.0.0.1:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: 'demo-app-release', 
                    version: '1.0.0'
                }


            }


        }
        
 }


}

