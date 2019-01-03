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
        sh 'println ${network}'
        sh 'println ${network1}'
      }
    }
  }
}
