pipeline {
  agent {
    kubernetes {
      defaultContainer 'kaniko'
      yaml '''
kind: Pod
spec:
  containers:
  - name: kaniko
    image: gcr.io/kaniko-project/executor:debug-a2aae6274dd5805bb9ca60c392a7f2d0a33c4045
    imagePullPolicy: Always
    command:
    - /busybox/cat
    tty: true
    volumeMounts:
      - name: jenkins-docker-cfg
        mountPath: /kaniko/.docker
  volumes:
  - name: jenkins-docker-cfg
    projected:
      sources:
      - secret:
          name: regcred
          items:
            - key: .dockerconfigjson
              path: config.json
'''
    }

  }
  stages {
    stage('Build') {
      parallel {
        stage('Build') {
          steps {
            sh 'ls'
          }
        }

        stage('Sonar scan') {
          steps {
            sh 'ls'
          }
        }

      }
    }

    stage('Push image') {
      steps {
        sh '/kaniko/executor -f `pwd`/Dockerfile -c `pwd` --insecure --skip-tls-verify --cache=true --destination=robeferre/golang-sample'
      }
    }

    stage('Deploy Dev') {
      steps {
        sh 'ls'
      }
    }

    stage('Load test') {
      parallel {
        stage('Load test') {
          steps {
            sh 'ls'
          }
        }

        stage('Security test') {
          steps {
            sh 'ls'
          }
        }

        stage('Integration test') {
          steps {
            sh 'ls'
          }
        }

      }
    }

  }
}