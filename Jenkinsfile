#!groovy

pipeline {
    agent any
    environment {
        registry = '160357565307.dkr.ecr.us-west-2.amazonaws.com/railsapp:latest'
        dockerImage = ''
    }
    stages {
        stage("Checkout") {
            steps {
                    git branch: 'master',
                        credentialsId: 'github',
                        url: 'https://github.com/bbsahoobyndr/eks-demo.git'
                        
                
                 }
        }
        
        stage("Docker Build") {  
             agent {
              docker 'mydocker'
        }
            steps {
                sh "docker build -t railsapp:latest ."
            }
            }
        stage("ECR Login") {
            steps {
                withAWS(credentials:'aws-credential') {
                    script {
                        def login = ecrLogin()
                        sh "${login}"
                    }
                }
            }
        }
        stage("Docker Push") {
            steps {
                sh "docker push ${registry}"
            }
        }
    }
    post {
        success {
            echo 'ending'
            build job: 'TestJob-CD'
        }
    }
}
