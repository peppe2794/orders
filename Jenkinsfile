pipeline {
  tools {
    nodejs 'NodeJS'
 }
  agent any
  stages {
     stage('Build'){
      agent {
        docker {
          image 'maven:3.6-jdk-11' 
          args '-v /var/lib/jenkins/workspace/order:/usr/src/mymaven -w /usr/src/mymaven -w /var/lib/jenkins/workspace/order -v /var/lib/jenkins/workspace/order:/var/lib/jenkins/workspace/order:rw,z -v /var/lib/jenkins/workspace/order@tmp:/var/lib/jenkins/workspace/order@tmp:rw,z' 
          reuseNode true
        }
      }
      steps{
         sh 'mvn -q -DskipTests package'
      }
    }
    stage('SonarQube analysis'){
      steps{
        withSonarQubeEnv(installationName: 'Sonarqube2', credentialsId: 'Sonarqube2') {
          sh "${tool("sonar_scanner")}/bin/sonar-scanner"
        }
      }
    }
  }
}
