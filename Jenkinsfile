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
        stage("SonarQube Status"){
            when {
                branch "featureone"
            }
            steps{
               timeout(time: 1, unit: 'HOURS') {
                //    For this to work, we should add webhook in sonar
                //    http://172.31.3.50:8080/sonarqube-webhook/
                    script{
                        def qg = waitForQualityGate()
                    if (qg.status != 'OK') {
                        error "Pipeline aborted due to quality gate failure: ${qg.status}"
                    }
                    }
                }
            }
        }
        stage("nexus upload"){
            when {
                branch "featureone"
            }
            steps{
                script{

                     def pomFile = readMavenPom file: 'pom.xml'
                     nexusArtifactUploader artifacts: [[artifactId: 'myweb', classifier: '', file: "target/myweb-${pomFile.version}", type: 'war']], credentialsId: 'nexus3', groupId: 'in.javahome', nexusUrl: '172.31.8.173:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'my-app', version: '0.0.6'
                 }
        }
        
        }
    }
}
}
/*def qg = waitForQualityGate()
                    if (qg.status != 'OK') {
                        error "Pipeline aborted due to quality gate failure: ${qg.status}"
                    }
*/
