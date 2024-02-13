pipeline {
    agent any 
    environment {
        DOCKERHUB_CREDENTIALS = credentials('chaimaekh-dockerhub')
    }
    stages {
        stage('Build') {
            steps {
                script {
                    sh 'docker build -t chaimaekh/dp-alpine:latest .'
                }
            }
        }
        stage('Login') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'chaimaekh-dockerhub', passwordVariable: 'DOCKERHUB_CREDENTIALS_PSW', usernameVariable: 'DOCKERHUB_CREDENTIALS_USR')]) {
                        sh "echo \$DOCKERHUB_CREDENTIALS_PSW | docker login -u \$DOCKERHUB_CREDENTIALS_USR --password-stdin"
                        echo 'Login successful'
                    }
                }
            }
        }
        stage('Push') {
            steps {
                script {
                    sh 'docker push chaimaekh/dp-alpine:latest'
                }
            }
        }
    }
    post {
        always {
            script {
                sh 'docker logout'
            }
        }
    }
}
