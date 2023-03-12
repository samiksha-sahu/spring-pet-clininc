pipeline {
  agent any
  tools {
    maven '3.6.0' 
  }
  stages {
    stage ('Build') {
      steps {
        sh 'mvn -version'
        //sh 'mvn clean install spring-boot:repackage'
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
