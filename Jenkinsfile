pipeline{
	
	agent any


	stages {

		stage('Build') {
			steps {
			    sshagent(credentials: ['aws']) {
                    sh 'ssh -o StrictHostKeyChecking=no ec2-user@44.211.185.222 "docker ; docker ps"'

                }
			   
			}
		}
		
	
	}
	}
