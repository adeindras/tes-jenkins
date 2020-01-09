pipeline {
  agent any
  stages {
    stage('Checkout Source') {
      steps {
        git 'https://github.com/adeindras/tes-jenkins.git'
      }
    }

    stage('Build image') {
      steps {
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }

      }
    }

    stage('Push Image') {
      steps {
        script {
          docker.withRegistry( "" ) {
            dockerImage.push()
          }
        }

      }
    }

    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "myweb.yaml", kubeconfigId: "tes-jenkins")
        }

      }
    }

  }
  environment {
    registry = '192.168.26.44:5000/myimage/mywebade'
    dockerImage = ''
  }
}