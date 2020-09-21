pipeline {
  agent {
    kubernetes {
      //cloud 'kubernetes'
      yaml """
kind: Pod
metadata:
  name: img
spec:
  containers:
  - name: img
    image: docker:1.11
    imagePullPolicy: Always
    command:
    - cat
    tty: true
     volumeMounts:
    - name: dockersock
      mountPath: /var/run/docker.sock
  volumes:
  - name: dockersock
    hostPath:
      path: /var/run/docker.sock
"""
    }
  }
  stages {
    stage('Build with Img') {
      environment {
        PATH = "/home/user/bin:$PATH"
      }
      steps {
        git 'https://github.com/bbsahoobyndr/eks-demo.git'
        container(name: 'img') {
            sh 'wget https://amazon-ecr-credential-helper-releases.s3.us-east-2.amazonaws.com/0.3.1/linux-amd64/docker-credential-ecr-login'
            sh 'chmod +x docker-credential-ecr-login'
            sh 'mkdir ~/bin'
            sh 'mv docker-credential-ecr-login ~/bin/docker-credential-ecr-login'
            sh '''
            img build . -t 160357565307.dkr.ecr.us-west-2.amazonaws.com/railsapp:latest -t 160357565307.dkr.ecr.us-west-2.amazonaws.com/railsapp:vImg$BUILD_NUMBER
            '''
            sh ' img push 160357565307.dkr.ecr.us-west-2.amazonaws.com/railsapp:latest'
            sh ' img push 160357565307.dkr.ecr.us-west-2.amazonaws.com/railsapp:vImg$BUILD_NUMBER'
        }
      }
    }
  }
}
