pipeline {
  agent any
  tools {
    maven '3.0.2' 
  }
  stages {
    stage ('Build') {
      steps {
        sh 'mvn clean package'
      }
    }
  }
}
