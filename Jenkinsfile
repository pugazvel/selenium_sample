def network='jenkins-${BUILD_NUMBER}'

pipeline {
  agent {
    node {
      label 'AppServer'
    }

  }
  stages {
    stage('Build Jar') {
      steps {
        sh 'echo ${network}'
      }
    }
  }
}
