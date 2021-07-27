pipeline {
  agent { label 'linux' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    registryName = 'TempTestCICD'
    //- update your credentials ID after creating credentials for connecting to ACR
    registryCredential  = 'ACR'
    dockerImage = ''
    registryUrl = 'temptestcicd.azurecr.io'
  }
  stages {
    stage('publish docker') {
      steps{
        script{
        docker.withRegistry("http://${registryUrl}", registryCredential) {
          def   dockerImage = docker.build("temptestcicd.azurecr.io/threeshape.nanoserver:1903-nanoserver-amd64")
          dockerImage.push 'latest'
        }
      }
    }
  }
  }
}
