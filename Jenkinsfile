def props = new Properties()
fileLoader.fromFile('config.properties').withInputStream { props.load(it) }

def datacenters = [props.'datacenter.sp', props.'datacenter.cp']
def environments = [
    props.'environment.preprod-sp-e2eperf',
    props.'environment.nonprod',
    props.'environment.preprod-sp',
    props.'environment.preprod-cp-e2eperf',
    props.'environment.bci-cp',
    props.'environment.bci-sp'
]
pipeline {
  agent any
  tools {
    maven '3.8.3' 
  }
  parameters {
        choice(
            name: 'datacenter',
            choices: datacenters,
            description: 'Select the data center'
        )
        choice(
            name: 'environment',
            choices: environments.grep { it.contains(params.datacenter) },
            description: 'Select the environment'
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
