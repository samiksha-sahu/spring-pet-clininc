properties([[$class: 'ParametersDefinitionProperty', parameterDefinitions: [[$class: 'ChoiceParameterDefinition', choices: ['cp', 'sp'], description: 'Select datacenter', name: 'datacenter'], [$class: 'ChoiceParameterDefinition', choices: environments."${params.datacenter}".split(','), description: 'Select environment', name: 'environment']]]])

def props = readProperties file: 'config.properties'
def datacenters = props.getProperty('datacenters').split(',')
def environments = props.getProperty('environments')

pipeline {
  agent any
  tools {
    maven '3.8.3' 
  }
  parameters {
        choice(
            name: 'datacenter',
            choices: datacenters,
            description: 'Select datacenter'
        )
        
        choice(
            name: 'environment',
            choices: environments."${params.datacenter}".split(','),
            description: 'Select environment'
               )
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
