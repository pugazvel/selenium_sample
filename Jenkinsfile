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
        sh '''sh "docker network create ${network}"
sh "docker run -d -p 4444:4444 --name ${seleniumHub} --network ${network} selenium/hub"
sh "docker run -d -e HUB_PORT_4444_TCP_ADDR=${seleniumHub} -e HUB_PORT_4444_TCP_PORT=4444 --network ${network} --name ${chrome} selenium/node-chrome"
sh "docker run -d -e HUB_PORT_4444_TCP_ADDR=${seleniumHub} -e HUB_PORT_4444_TCP_PORT=4444 --network ${network} --name ${firefox} selenium/node-firefox"'''
      }
    }
  }
}