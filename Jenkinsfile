podTemplate(yaml: """
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: centos7
    image: centos7
    command: ['cat']
    tty: true
    volumeMounts:
    - name: dockersock
      mountPath: /var/run/docker.sock
  volumes:
  - name: dockersock
    hostPath:
      path: /var/run/docker.sock
"""
  ) {
  node(POD_LABEL) {
    stage('Build Docker image') {
     // git 'https://github.com/jenkinsci/docker-jnlp-slave.git'
      container('docker') {
        sh "echo hello world"
      }
    }
  }
}
