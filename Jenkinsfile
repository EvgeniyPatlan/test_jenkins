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
        sh 'mkdir test'
      }
    }
  }
}