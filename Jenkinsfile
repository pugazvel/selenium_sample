pipeline {
  agent {
    node {
      label 'AppServer'
    }

  }
  stages {
    stage('Build Jar') {
      steps {
        sh 'echo ${params.network}'
      }
    }
  }
  environment {
        NETWORK = 'jenkins-${BUILD_NUMBER}'
    }
}
