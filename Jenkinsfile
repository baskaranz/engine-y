pipeline {
  environment {
    imageName = 'beswaran/nginx'
    registryCredential = 'dockerhub'
    registryUrl = 'https://registry.hub.docker.com'
    repositoryCredential = 'github'
    repositoryUrl = 'https://github.com/baskaranz/engine-y.git'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git([url: repositoryUrl, branch: 'master', credentialsId: repositoryCredential])
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build imageName + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry('https://registry.hub.docker.com', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
  }
}
