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
          args '-v /var/lib/jenkins/workspace/orders:/usr/src/mymaven -w /usr/src/mymaven -w /var/lib/jenkins/workspace/orders -v /var/lib/jenkins/workspace/orders:/var/lib/jenkins/workspace/orders:rw,z -v /var/lib/jenkins/workspace/orders@tmp:/var/lib/jenkins/workspace/orders@tmp:rw,z' 
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
