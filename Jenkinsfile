pipeline {
  agent any
  stages {
    stage('Get Sources') {
      agent any
      steps {
        sh 'echo "Deploying to ${product}"'
      }
    }
  }
  parameters {
    string(name: 'product', defaultValue: 'percona-server-5.6', description: '')
  }
}