podTemplate(
  label: agent_label,
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
  node(agent_label) {
    stage('test') {
      container('centos') {
        sh "echo hello"
      }
    }
  }
    
      
