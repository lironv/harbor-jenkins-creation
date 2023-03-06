
pipeline {
  agent any  
  stages {
     
    stage('Build image') {        
      steps {
          withCredentials([dockerRegistryCredentials(credentialsId: 'docker-creds', url: 'https://core.harbor.domain')]) {
            docker.build("my-image:${env.BUILD_ID}")
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




