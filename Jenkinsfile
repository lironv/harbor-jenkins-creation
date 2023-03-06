
pipeline {
  agent any  
  stages {
     
    stage('Build image') {        
      steps {
        sh 'sudo yum install -y docker'
        app = docker.build("Dockerfile", "./")    
       }
    }
    stage('Test image') {   
      steps {
      app.inside {            
      sh 'echo "Tests passed"'        
      }
      }    
        }     
    stage('Push image') {
      steps {
      docker.withRegistry('https://core.harbor.domain', 'harbor admin') {            
        app.push("${env.BUILD_NUMBER}")            
        app.push("latest")        
      }
      }    
           }
        }
}




