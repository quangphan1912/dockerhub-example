pipeline {
  agent { label 'linux' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('docker-hub')
  }
   stages {
    stage('Build') {
      steps {
        sh 'docker build -t quangphan1912/dp-alpine3:latest .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push quangphan1912/dp-alpine3:latest'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}