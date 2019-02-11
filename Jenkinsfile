pipeline {
  agent any
  stages {
    stage('Get Sources') {
      agent any
      steps {
        sh '''BRANCH=$(echo ${PRODUCT} | sed -e \'s/percona-server-//\')
wget https://raw.githubusercontent.com/Percona-Lab/ps-build/${BRANCH}/docker/install-deps
ls -la'''
      }
    }
  }
  parameters {
    choice(choices: '''percona-server-5.6
percona-server-5.7
percona-server-8.0''', description: 'What product should be tested?', name: 'PRODUCT')
    choice(choices: '''experimental
testing''', description: 'What repo should be used?', name: 'REPO')
  }
}