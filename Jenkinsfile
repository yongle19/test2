pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '-p 3011:3000'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }

    stage('Test') {
      environment {
        CI = 'true'
      }
      steps {
        sh 'sh ./jenkins/scripts/test.sh'
      }
    }

    stage('Deliver') {
      steps {
        sh 'sh ./jenkins/scripts/deliver-for-development.sh'
        input 'Finished using the web site? (Click "Proceed" to continue)'
        sh 'sh ./jenkins/scripts/kill.sh'
      }
    }

  }
}