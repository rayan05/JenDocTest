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
    stage('Build') {
      steps {
        sh 'docker build -t temptestcicd.azurecr.io/dp-alpine:latest .'
      }
    }
    stage('publish docker') {
      steps{
        script{
        docker.withRegistry("http://${registryUrl}", registryCredential) {
            docker.push temptestcicd.azurecr.io/dp-alpine:latest
        }
      }
    }
  }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
