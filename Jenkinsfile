pipeline {
  environment {
    registry = "peppe2794/frontend"
    registryCredential = 'dockerhub'
    dockerImage = ''
    DOCKER_TAG = getVersion().trim()
    IMAGE="frontend"
  }
  tools {
    nodejs 'NodeJS'
 }
  agent any
  stages {
    stage('SonarQube analysis'){
      steps{
        withSonarQubeEnv(installationName: 'Sonarqube2', credentialsId: 'Sonarqube2') {
          sh "${tool("sonar_scanner")}/bin/sonar-scanner"
        }
      }
    }
  }
}
