pipeline {
  agent {
    kubernetes {
      yaml '''
        apiVersion: v1
        kind: Pod
        spec:
          securityContext:
            runAsUser: 1000
          containers:
          - name: kubectl
            image: bitnami/kubectl:latest
            command:
            - sleep
            args:
            - 99d
            tty: true
            securityContext:
              privileged: true

        '''
    }
  }

  stages {
    stage('Deploy deploy to eks') {
      steps {
        container('kubectl') {
          sh '''
           kubectl apply -f app-deploy.yaml -n master
           kubectl apply -f consumer-deploy.yaml -n master
          '''
        }
      }
    }
  }
}
