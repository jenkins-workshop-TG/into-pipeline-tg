pipeline {
  agent {
    label 'jdk8'
  }
  stages {
    stage('Say Hello') {
      steps {
        echo "Hello ${MY_NAME}"
        echo "${TEST_USR_USR}"
        echo "${TEST_USR_PSW}"
        sh 'java -version'
      }
    }
  }
  environment {
    MY_NAME = 'Terry'
    TEST_USR = credentials('test-user')
  }
}