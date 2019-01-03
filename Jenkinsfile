pipeline {
  agent {
    node {
      label 'AppServer'
    }

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
        sh 'docker run -d -p 4444:4444 --name selenium-hub-${BUILD_NUMBER} --network jenkins-${BUILD_NUMBER} selenium/hub'
        sh 'docker run -d -e HUB_PORT_4444_TCP_ADDR=selenium-hub-${BUILD_NUMBER} -e HUB_PORT_4444_TCP_PORT=4444 --network jenkins-${BUILD_NUMBER} --name chrome-${BUILD_NUMBER} selenium/node-chrome'
        sh 'docker run -d -e HUB_PORT_4444_TCP_ADDR=selenium-hub-${BUILD_NUMBER} -e HUB_PORT_4444_TCP_PORT=4444 --network jenkins-${BUILD_NUMBER} --name firefox-${BUILD_NUMBER} selenium/node-firefox'
      }
    }
    stage('Run Test') {
      steps {
        sh 'docker run --rm -e SELENIUM_HUB=selenium-hub-${BUILD_NUMBER} -e BROWSER=firefox -e MODULE=search-module.xml -v ${WORKSPACE}/search:/usr/share/tag/test-output --network jenkins-${BUILD_NUMBER} velraja/containertest archiveArtifacts artifacts: \'search/**\', fingerprint: true'
      }
    }
  }
}