pipeline {
  agent any
  tools {
    maven '3.0.2' 
  }
  stages {
    stage ('Build') {
      steps {
        sh 'mvn -version'
        sh 'mvn clean package'
      }
    }
     stage("Sonar") {
       steps {
         sh 'mvn sonar:sonar'
            }
        }
  }
}
