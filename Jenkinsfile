podTemplate(
  containers: [
    containerTemplate(
      name: 'jnlp-slave',
      image: 'jenkins/jnlp-slave',
      command: 'cat',
      ttyEnabled: true
      )
    ],
    volumes: [
      hostPathVolume(hostPath: '/var/run/docker.sock', mountPath: '/var/run/docker.sock')
      ]
) {
  node(POD_LABEL) {
    stage('test') {
      container('jnlp-slave') {
        sh "echo hello"
      }
    }
  }
}
    
      
