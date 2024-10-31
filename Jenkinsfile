pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/KIM1234567/jenkinstest.git', branch: 'main'
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
        sudo docker build -t dhdtl12/keduitlab:purple .
        sudo docker push dhdtl12/keduitlab:purple
        '''
      }
    }
    stage('deploy and service') {
      steps {
        sh '''
         ansible master -m shell -a "sudo kubectl create deploy web-${now} --replicas=3 --port=80 --image=dhdtl12/keduitlab:${now}"
        ansible master -m shell -a "sudo kubectl expose deploy web-${now} --type=LoadBalancer --port=80 --target-port=80 --name=web-${now}-svc"

        '''
      }
    }
  }
}
