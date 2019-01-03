pipeline {
  agent {
    node {
      label 'AppServer'
    }
  }
  environment {
    network='jenkins-${BUILD_NUMBER}'
    seleniumHub='selenium-hub-${BUILD_NUMBER}'
    chrome='chrome-${BUILD_NUMBER}'
    firefox='firefox-${BUILD_NUMBER}'
    containertest='conatinertest-${BUILD_NUMBER}'
  }
  stages {
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
        sh 'docker network create jenkins-${BUILD_NUMBER}'
      }
    }
  }
}
