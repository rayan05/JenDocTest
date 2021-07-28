pipeline {
  agent { label 'windows2004-docker-production-1' }
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
             println "******************************************************" 
             def  st = new Date()
              println st.format("yyMMdd.HHmm", TimeZone.getTimeZone('UTC'))
              
              docker.withRegistry("http://${registryUrl}", registryCredential) {
                  def   dockerImage = docker.build("temptestcicd.azurecr.io/threeshape.nanoserver:1903-nanoserver-amd64")
                  dockerImage.push 'latest'
              }
               def delta = (new Date()).getTime() - st.getTime()
               def seconds = delta.intdiv(1000) % 60
               def minutes = delta.intdiv(60 * 1000) % 60
                    
               println "${minutes} min ${seconds} sec" 
               println "******************************************************" 
        }
    }
  }
  }
}
