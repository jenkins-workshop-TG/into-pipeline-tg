pipeline {
  agent {
    label 'jdk9'
  }
  stages {
    stage('Say Hello') {
      steps {
        echo "Hello ${params.Name}"
        echo "Name defined as ${MY_NAME}"
        echo "${TEST_USR_PSW}"
        sh 'java -version'
      }
    }
  }
  environment {
    MY_NAME = 'Terry'
    TEST_USR = credentials('test-user')
  }
  parameters {
    string(name: 'Name', defaultValue: 'whoever you are', description: 'Who should I say hi to?')
  }
}