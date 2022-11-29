pipeline {

  environment {
    dockerimagename = "praveensingam1994/nodeapp"
    dockerImage = ""
    
  }

  agent any
  tools {dockerTool  "MyDocker" } 
  stages {
    
//     stage('Build Container') {
//       steps {
//         echo 'Building Container..'
//                 script {
//                     def dockerHome = tool 'MyDocker'
                       env.PATH = "${dockerHome}/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:${env.PATH}"
                       
          
//                 }
//       }
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
          sh "docker images"
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
          dockerImage.push("${dockerimagename}")
          }
        }
      }
    }

//     stage('Deploying App to Kubernetes') {
//       steps {
//         script {
//           sh '''#!/bin/bash
//           eval $(minikube -p minikube docker-env)
//           '''
//           kubernetesDeploy(configs: "deploymentservice.yml", kubeconfigId: "kubernetes")
//         }
//       }
//     }

  }

}
