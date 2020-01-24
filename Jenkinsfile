pipeline {
  agent {
    kubernetes {
      yaml """
apiVersion: v1
kind: Pod
metadata:
  labels:
    some-label: some-label-value
spec:
  volumes:
  - name: docker
    hostPathVolume:
      hostPath: '/var/run/docker.sock'
      mountPath: '/var/run/docker.sock'
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
