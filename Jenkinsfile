def properties = readProperties file: 'config.properties'


pipeline {
  agent any
  tools {
    maven '3.8.3' 
  }
  // Get the available data centers from the properties file
def datacenters = properties.getProperty('datacenters').split(',')

// Define the parameters
parameters {
    // Dropdown list for data center
    choice(name: 'datacenter', choices: datacenters, description: 'Select data center')
}

// Read the selected data center from the build parameters
def datacenter = params.datacenter

// Get the available environments for the selected data center from the properties file
def environments = properties.getProperty(datacenter).split(',')

// Define the parameters
parameters {
    // Dropdown list for environment
    choice(name: 'environment', choices: environments, description: 'Select environment')
}
  stages {
    stage ('Build') {
      steps {
        sh 'mvn -version'
       // sh 'mvn clean install spring-boot:repackage
        sh 'mvn spring-javaformat:apply'
       sh 'mvn clean package'
      //  sh 'mvn clean'
        //sh 'mvn package'
      }
    }
     stage("Sonar") {
       steps {
         sh 'mvn sonar:sonar'
            }
        }
  }
}
