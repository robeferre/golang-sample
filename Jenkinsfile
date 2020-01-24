pipeline {
  agent {
    kubernetes {
      yaml """
apiVersion: v1
kind: Pod
metadata:
  labels:
    some-label: some-label-value
volumes:
  - hostPathVolume
      hostPath: '/var/run/docker.sock'
      mountPath: '/var/run/docker.sock'
spec:
  containers:
  - name: maven
    image: maven:alpine
    command:
    - cat
    tty: true
  - name: docker
    image: docker
    command:
    - cat
    tty: true
    privileged: true
"""
    }
  }
  stages {
    stage('Run maven') {
      steps {
        container('maven') {
          sh 'mvn -version'
        }
        container('docker') {
          sh 'docker ps'
        }
      }
    }
  }
}
