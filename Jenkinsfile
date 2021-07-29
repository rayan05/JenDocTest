pipeline {
  agent { label 'windows2004-docker-production-1' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    registryName = 'temptestcicd.azurecr.io/threeshape.nanoserver:1903-nanoserver-amd64'
    registryCredential  = 'ACR'
    dockerImage = ''
    registryUrl = 'temptestcicd.azurecr.io'
  }
  stages {
    stage('publish docker') {
      steps{
        script{
              docker.withRegistry("http://${registryUrl}", registryCredential) {
                def   dockerImage = docker.build("${registryName}")
                dockerImage.push 'latest'
              }
        }
      }
    }
  }
}
