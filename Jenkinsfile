pipeline {
  agent {
    node {
      label 'AppServer'
    }

  }
  stages {
    stage('Build Jar') {
      steps {
        sh '''echo ${network}
echo ${env.network}'''
      }
    }
  }
}