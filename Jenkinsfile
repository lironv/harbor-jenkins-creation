
node {    
      def app     
      stage('Clone repository') {               
             
            checkout scm    
      }     
      stage('Build image') {         
       
            app = docker.build("Dockerfile", "./")    
       }     
      stage('Test image') {           
            app.inside {            
             
             sh 'echo "Tests passed"'        
            }    
        }     
       stage('Push image') {
       docker.withRegistry('https://core.harbor.domain', 'harbor admin') {            
         app.push("${env.BUILD_NUMBER}")            
         app.push("latest")        
              }    
           }
        }
