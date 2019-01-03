def network="jenkins-${BUILD_NUMBER}"
def network1='jenkins'

pipeline {
  agent {
    node {
      label 'AppServer'
    }

  }
  stages {
    stage('Build Jar') {
      steps {
        sh 'echo velraja'
        sh 'echo ${BUILD_NUMBER}'
        sh 'echo ${network}'
        sh 'echo ${network1}'
      }
    }
  }
}
