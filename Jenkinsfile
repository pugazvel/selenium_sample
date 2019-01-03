pipeline {
  agent {
    node {
      label 'AppServer'
    }

  }
  stages {
    stage("make param global") {
       steps {
         tmp_param =  sh (script: 'jenkins-${BUILD_NUMBER}', returnStdout: true).trim()
         env.network = tmp_param
        }
    }
    stage('Build Jar') {
      steps {
        sh 'mvn clean package -DskipTests'
      }
    }
    stage('Build Image') {
      steps {
        script {
          app = docker.build("velraja/containertest")
        }

      }
    }
    stage('Push Image') {
      steps {
        script {
          docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${BUILD_NUMBER}")
            app.push("latest")
          }
        }

      }
    }
    stage('Setting Up Selenium Grid') {
      steps {
        sh 'docker network create ${env.network}'
      }
    }
  }
}
