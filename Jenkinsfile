pipeline {
  agent {
    node {
      label 'AppServer'
    }

  }
  parameters {
        string(name: 'network', defaultValue: 'jenkins-${BUILD_NUMBER}', description: '')
  }
  stages {
    stage('Build Jar') {
      steps {
        sh 'echo ${network}'
      }
    }
  }
}
