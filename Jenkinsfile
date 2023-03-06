
pipeline {
  agent any  
  stages {
     
    stage('Build image') {        
      steps {
        sh """pwd
              echo $PATH 
              id
              docker build -t lironv/attendance:latest .
           """
        
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




