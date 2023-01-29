pipeline{
    agent any
    triggers {
      pollSCM '* * * * *'
    }
    tools {
         maven 'maven3'
        }
    stages{
        stage("Maven unittesting"){
            when {
                branch "featureone"
            }
            steps{
               sh "mvn test"
            }
        }
        stage("Maven integration"){
            when {
                branch "featureone"
            }
            steps{
               sh "mvn verify -DskipUnitTests=true"
            }
        }
        
        stage("Maven Build"){
            when {
                branch "featureone"
            }
            steps{
               sh "mvn clean install"
            }
        }
        stage("SonarQube Analysis"){
            when {
                branch "featureone"
            }
            steps{
               withSonarQubeEnv('sonar7') {
                    sh "mvn sonar:sonar"
               }
            }
        }
        
        }
    }
