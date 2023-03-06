
pipeline {
  agent any  
  stages {
     
    stage('Build image') {        
      steps {
      withDockerContainer('my-image') {
          sh 'docker build -t image:$BUILD_NUMBER .'
      }            
           
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




