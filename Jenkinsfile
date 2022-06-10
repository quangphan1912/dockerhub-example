pipeline {
  agent { label 'linux' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  }
    stages {
      stage('check') {
      steps {
        sh 'sudo chmod 666 /var/run/docker.sock'
        sh 'Hitachi@123'
        sh 'pwd'
      }
    }
    stage('Build') {
      steps {
        sh 'docker build -t quangphan1912/dp-alpine:latest .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push quangphan1912/dp-alpine:latest'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
//     always {
//             echo "ALWAYS THE SUN!!!"
//             junit '**/nonexisting_to_make_this_fail/*.xml'
//         }
//         failure {
//             echo "WE FAILED MISERABLY! I won't be shown because junit step failed above"
//         }
  }
}
