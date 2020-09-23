podTemplate(
  containers: [
    containerTemplate(
      name: 'centos',
      image: 'centos:centos7',
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
      container('centos') {
        sh "echo hello"
      }
    }
  }
}
    
      
