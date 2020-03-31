pipeline {

  environment {
    registry = "192.168.1.2:5000/justme/myweb"
    dockerImage = ""
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/longhoang0305/playjenkins.git'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build registry + "1"
        }
      }
    }

    stage('Push Image') {
      steps{
        script {
          docker.withRegistry( "https://192.168.1.2:5000", "docker-credential" ) {
            dockerImage.push()
          }
        }
      }
    }

    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "myweb.yaml", kubeconfigId: "mykubeconfig")
        }
      }
    }

  }

}
