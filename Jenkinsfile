pipeline{
    agent any
    triggers {
      pollSCM '* * * * *'
    }
    tools {
         maven 'maven3'
        }
    stages{
        stage("Maven Build"){
            when {
                branch "featureone"
            }
            steps{
               sh "mvn package"
            }
        }
        
        }
    }
