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
    stage('Install deps') {
      agent any
      steps {
        sh 'echo "sudo bash -x ./install-deps"'
      }
    }
    stage('Install repo') {
      agent any
      steps {
        sh '''wget https://repo.percona.com/percona/apt/percona-release_1.0-7.generic_all.deb
echo "sudo dpkg -i percona-release_1.0-7.generic_all.deb"
BRANCH=$(echo ${PRODUCT} | sed -e \'s/percona-server-//\')
if [ ${BRANCH} = 8.0 ]; then
  echo "sudo percona-release enable ps-80 ${REPO}"
else
  echo "sudo percona-release enable original${REPO}"
fi
echo "sudo apt update"'''
      }
    }
    stage('Install product') {
      agent any
      steps {
        sh '''VERSION=$(echo ${PRODUCT} | sed -e \'s/percona-server-//\')
if [ ${VERSION} = 8.0 ]; then
  INSTALL_LIST="percona-server-server percona-server-dbg percona-server-test"
else
  INSTALL_LIST="percona-server-${VERSION} percona-server-test-${VERSION}"
fi
echo "sudo apt-get -y install ${INSTALL_LIST}"'''
      }
    }
    stage('Run test') {
      steps {
        sh 'echo "cd /usr/share/mysql-test/ && ./mysql-test/mtr --suite=innodb"'
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