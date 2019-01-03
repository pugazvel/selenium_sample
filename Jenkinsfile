pipeline {
  agent {
    node {
      label 'AppServer'
    }

  }
  stages {
    stage('Build Jar') {
      steps {
        sh '''def network=\'jenkins-${BUILD_NUMBER}\'
echo ${network}'''
      }
    }
  }
}