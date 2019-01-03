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
  parameters {
    string(name: 'network', defaultValue: 'jenkins-${BUILD_NUMBER}', description: '')
  }
}