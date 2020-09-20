#!groovy
pipeline {
    agent {

    kubernetes {

        defaultContainer 'jnlp'
        yamlFile 'agentpod.yaml'
    }
}
stages {
    stage('Build') {
        steps {
            container('maven') {
                sh 'mvn package'
            }
        }
    }
    stage('Docker Build') {

        steps {
            container('docker') {
                sh "docker build -t dockerimage ."
            }
        }
    }
    
}
}
