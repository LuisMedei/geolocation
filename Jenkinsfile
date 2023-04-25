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
    }
}