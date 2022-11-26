pipeline {

  environment {
    dockerimagename = "praveensingam1994/nodeapp"
    dockerImage = ""
  }
  tools {
    docker "MyDocker"
  }


  agent any

  stages {
    
//     stage('Initialize') {
//       def docker = tool 'MyDocker'
//       env.PATH = "${docker}/bin:${env.PATH}"
//     }
    
    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build dockerimagename
        }
      }
    }

    stage('Pushing Image') {
      environment {
               registryCredential = 'dockerhubcred'
           }
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
            dockerImage.push("latest")
          }
        }
      }
    }

    stage('Deploying App to Kubernetes') {
      steps {
        script {
          kubernetesDeploy(configs: "deploymentservice.yml", kubeconfigId: "kubernetes")
        }
      }
    }

  }

}
