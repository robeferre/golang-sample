pipeline {
  agent {
    kubernetes {
      yaml """
apiVersion: v1
kind: Pod
metadata:
  labels:
    docker: true
spec:
  containers:
  - name: docker
    image: docker:latest
    privileged: true
    workingDir: '/home/jenkins/agent',
    command:
    - cat
    tty: true
  - name: maven
    image: maven:alpine
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
