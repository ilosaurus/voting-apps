pipeline {
  agent none
  stages{
    stage('docker-package'){
          agent any
          when{
            branch 'master'
          }
          steps{
            echo 'Deploy instavote app with docker compose'
            sh 'docker-compose down --remove '
            sh 'docker-compose up -d'
          }
      }
  }
  post{
    always{
      echo 'Building multibranch pipeline for worker is completed..'
    }
    failure {
      slackSend (channel: "instavoteg2", message: "Build Failed - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)")
    }
    success {
      slackSend (channel: "instavoteg2", message: "Build Succeeded - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)")
    }
  }
}
