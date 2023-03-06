
pipeline {
  agent any  
  stages {
     
    stage('Build image') {        
      steps {
        sh 'yum install -y docker'
         script {
           app = docker.build("my-app-image:latest", "./")
          }
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




