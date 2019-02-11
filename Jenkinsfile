pipeline {
  agent any
  stages {
    stage('Get Sources') {
      agent any
      steps {
        sh 'echo "Testing ${PRODUCT} from ${REPO} repo"'
      }
    }
  }
  parameters {
    choice(choices: ['percona-server-5.6', 'percona-server-5.7', 'percona-server-8.0'], description: 'What product should be tested?', name: 'PRODUCT')
    choice(choices: ['experimental', 'testing'], description: 'What repo should be used?', name: 'REPO')
  }
}