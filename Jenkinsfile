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
    stage('Run latest container') {
      steps{
        script {
          docker.withRegistry('https://registry.hub.docker.com', registryCredential ) {
            sh "docker run -p 80:80 -d ${imageName}:latest"
          }
        }
      }
    }
  }
}
