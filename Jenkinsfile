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
                nexusArtifactUploader artifacts: [[artifactId: '${POM_ARTIFACTID}', 
                classifier: '', 
                file: 'target/${POM_ARTIFACTID}-${POM_VERSION}.${POM_PACKAGING}', 
                type: '${POM_PACKAGING}']], 
                credentialsId: 'NexusID', 
                groupId: '${POM_GROUPID}', 
                nexusUrl: '45.79.162.202:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: 'maven-nexus-repo', 
                version: '${POM_VERSION}'
            }
        }

    }
}