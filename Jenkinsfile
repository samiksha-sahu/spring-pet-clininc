def properties = readProperties file: 'config.properties'


pipeline {
  agent any
  tools {
    maven '3.8.3' 
  }
//   // Get the available data centers from the properties file
// def datacenters = properties.getProperty('datacenters').split(',')

// // Define the parameters
// parameters {
//     // Dropdown list for data center
//     choice(name: 'datacenter', choices: datacenters, description: 'Select data center')
// }

// // Read the selected data center from the build parameters
// def datacenter = params.datacenter

// // Get the available environments for the selected data center from the properties file
// def environments = properties.getProperty(datacenter).split(',')

// Define the parameters
  environment{
    TestEnv = "${environment}"
  }
   parameters {
         choice(
            name: 'environment',
            choices: ['nonprod', 'preprod', 'test'],
            description: 'Select an environment.'
        )
        choice(
            name: 'dataCenter',
            choices: ['aa', 'bb']
            description: 'Select a data center.'
        )
       
    }
  stages {
//     stage('Load Properties File') {
//             steps {
//                 script {
//                     def props = readProperties file: 'config.properties'
//                     echo "Data Centers: ${props.data_centers}"
//                     echo "Environments: ${props.environments}"
//                 }
//             }
//         }
    stage('Env credentials'){
      steps{
        // I have tested environment instead of steps/ scripts but nothing worked
        script{
          if( $'Testenv' == 'test' || 'nonprod'){
            sha_rsa = credential("monitoring_ansible_${environment}_private_key")
            sha_rsa1 = credential("apigee-ssh-key-${environment}")
          }
          else
          {
            sha_rsa = credential("monitoring_ansible_${environment}-${dataCenter}_private_key")
            sha_rsa1 = credential("apigee-ssh-key-${environment}-${dataCenter}"
          }
        }
      }
    }
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
