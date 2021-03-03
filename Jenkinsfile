pipeline {
  environment {
    imagename = "baskaranz/nginx"
    registryCredential = 'dockerhub'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git([url: 'https://github.com/baskaranz/engine-y.git', branch: 'master', credentialsId: 'github'])

      }
    }
    stage('Initialize'){
        def dockerHome = tool 'myDocker'
        env.PATH = "${dockerHome}/bin:${env.PATH}"
    }    
    stage('Check docker version') {
      steps{
        sh "docker version"
      }
    }    
  }
}