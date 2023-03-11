pipeline {
  agent {
    kubernetes {
      yaml '''
        apiVersion: v1
        kind: Pod
        spec:
          containers:
          - name: docker
            image: docker:latest
            command:
            - cat
            tty: true
            volumeMounts:
             - mountPath: /var/run/docker.sock
               name: docker-sock
          volumes:
          - name: docker-sock
            hostPath:
              path: /var/run/docker.sock    
        '''
    }
  }
  stages {
    
    stage('Build-Docker-Image') {
      steps {
        container('docker') {
          sh 'docker build -t sample-image:latest .'
          sh 'docker tag sample-image:latest lironv/testing-image:latest'
          sh 'docker tag sample-image:latest core.harbor.domain/jenkinspipe/image-push'


        }
      }
    }
    stage('Login-Into-Docker') {
      steps {
        container('docker') {
          sh 'docker login 10.110.211.191 -u lironv -p Qweasdzxc1'
      }
    }
    }
     stage('Push-Images-Docker-to-DockerHub') {
      steps {
        container('docker') {
          sh 'docker push core.harbor.domain/jenkinspipe/image-push'
      }
    }
     }
  }
    post {
      always {
        container('docker') {
          sh 'docker logout'
      }
      }
    }
}



















