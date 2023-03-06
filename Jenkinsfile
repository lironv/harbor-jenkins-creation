pipeline {
  agent any  
  stages {

    stage('Build image') {        
      steps {
        script {
          def customImage = docker.build("my-image:${env.BUILD_ID}")
        }

       }

    
          
            
    

          
    
    
  
    }
    stage('Test image') {   
      steps {
        script {
          customImage.inside {            
          sh 'echo "Tests passed"'        
          }
        }
      }    
        }     
    stage('Push image') {
      steps {
        script {
          docker.withRegistry('https://core.harbor.domain', 'harbor admin') {            
            customImage.push("${env.BUILD_NUMBER}")            
            customImage.push("latest")        
    } 
     }
      }    
           }
        }
}
