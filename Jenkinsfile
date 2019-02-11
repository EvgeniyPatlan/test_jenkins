pipeline {
  agent any
  stages {
    stage('Get Sources') {
      agent {
        docker {
          image 'centos:7'
        }

      }
      steps {
        sh 'echo "Deploying to ${product}"'
      }
    }
  }
  parameters {
    string(name: 'product', defaultValue: 'percona-server-5.6', description: '')
  }
}