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
                branch "develop"
            }
            steps{
               sh "mvn package"
            }
        }
        
        }
    }
