pipeline {
    triggers {
  pollSCM('* * * * *')
    }
   agent any
    tools {
  maven 'M2_HOME'
    }
    stages{
        stage('marvin build'){
            steps{
                sh 'mvn clean install package'
            }
        }
        stage('Upload Artifact to Nexus'){
            steps{
                script{
                def mavenPom = readMavenPom file: 'pom.xml'
                nexusArtifactUploader artifacts: [[artifactId: "${mavenPom.artifactId}", 
                classifier: '', 
                file: "target/${mavenPom.artifactId}-${mavenPom.version}.${mavenPom.packaging}", 
                type: "${mavenPom.packaging}"]], 
                credentialsId: 'NexusID', 
                groupId: "${mavenPom.groupId}", 
                nexusUrl: '45.79.162.202:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: 'maven-nexus-repo', 
                version: "${mavenPom.version}"
                }
            }
        }

    }
}