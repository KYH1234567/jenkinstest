pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/KYH1234567/jenkinstest.git', branch: 'master'
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
        sudo docker build -t dhdtl12/keduitlab:red .
        sudo docker push dhdtl12/keduitlab:red
        pwd
        '''
      }
    }
    stage('deploy and service') {
      steps {
        sh '''
        ansible-playbook /var/lib/jenkins/to_node.yml
        ansible-playbook /var/lib/jenkins/to_master.yml 
        '''
      }
    }
  }
}
