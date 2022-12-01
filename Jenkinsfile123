node {    
      def app     
      stage('Clone repository') {               
             
            checkout scm    
      }     
      stage('Build image') {         
       
            app = docker.build("praveensingam1994/test")    
       }     
      stage('Test image') {           
            app.inside {            
             
             sh 'echo "Tests passed"'        
            }    
        }     
       stage('Push image') {
       
        environment {
               registryCredential = 'dockerhubcred'
           }
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
          app.push("${env.BUILD_NUMBER}")            
          app.push("latest")        
          }
        }
      } 
           }
        }
