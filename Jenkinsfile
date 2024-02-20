pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/ARAOLGA/cicdtest.git', branch: 'main'
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
        sudo docker build -t kystic125/cicdtest:green .
        sudo docker push kystic125/cicdtest:green
        '''
      }
    }
    stage('deploy kubernetes') {
      steps {
        sh '''
        ansible master -m shell -a 'kubectl create deploy pl-bulk-prod --image=kystic125/cicdtest:green'
        ansible master -m shell -a 'kubectl expose deployment pl-bulk-prod --type=LoadBalancer --port=80 --target-port=80 --name=pl-bulk-prod-'
        '''
      }
    }
  }
}
