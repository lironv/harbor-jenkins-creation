
pipeline {
  agent any  
  stages {
     
    stage('Build image') {        
      steps {
        def customImage = docker.build("my-image:${env.BUILD_ID}")

        
       }
    }
    stage('Test image') {   
      steps {
        script {

          app.inside {            
          sh 'echo "Tests passed"'        
          }
        }
      }    
        }     
    stage('Push image') {
      steps {
        script {
          docker.withRegistry('https://core.harbor.domain', 'harbor admin') {            
            app.push("${env.BUILD_NUMBER}")            
            app.push("latest")        
    } 
     }
      }    
           }
        }
}




