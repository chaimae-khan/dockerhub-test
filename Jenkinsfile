pipeline {
  agent any 
  environment {
    DOCKERHUB_CREDENTIALS  = credentials('chaimaekh-dockerhub')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t chaimaekh/dp-alpine:latest .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
        echo'login acces '
      }
    }
    stage('Push') {
      steps {
        sh 'docker push chaimaekh/dp-alpine:latest'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
