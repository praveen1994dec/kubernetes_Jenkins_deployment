pipeline {

  environment {
    dockerimagename = "praveensingam1994/nodeapp"
    dockerImage = ""
    
  }

  agent any

  stages {
    
    stage('Build Container') {
      steps {
        echo 'Building Container..'
                script {
                    def dockerHome = tool 'MyDocker'
                    env.PATH = "${dockerHome}/bin:${env.PATH}"
          
                }
      }
    }
    
    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build dockerimagename
        }
      }
    }

    stage('Pushing Image') {
      environment {
               registryCredential = 'dockercred'
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
          sh '''#!/bin/bash
          eval $(minikube -p minikube docker-env)
          '''
          kubernetesDeploy(configs: "deploymentservice.yml", kubeconfigId: "kubernetes")
        }
      }
    }

  }

}
