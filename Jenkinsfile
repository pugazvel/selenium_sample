pipeline {
  agent {
    node {
      label 'AppServer'
    }

  }
  stages {
    stage('Build Jar') {
      steps {
        sh 'printenv'
      }
    }
  }
  environment {
    NETWORK = 'jenkins-${env.BUILD_NUMBER}'
  }
}
