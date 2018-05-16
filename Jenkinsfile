pipeline {
  agent {
    label 'jdk8'
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
    
    stage('Checkpoint') {
         agent none
         steps {
            checkpoint 'Checkpoint'
         }
      }    
    
    stage('Testing') {
        parallel {
          stage('Java 9') {
            agent { label 'jdk9' }
            steps {
              container('maven9') {
                sh 'mvn -v'
              }
            }
          }
          stage('Java 8') {
            agent { label 'jdk8' }
            steps {
              container('maven8') {
                sh 'mvn -v'
              }
            }
          }
        }
      }
    
    
   stage('Get Kernel') {
      steps {
        script {
          try {
            KERNEL_VERSION = sh (script: "uname -r", returnStdout: true)
          } catch(err) {
            echo "CAUGHT ERROR: ${err}"
            throw err
          }
        }
      }
    }
    
    stage('Say Kernel') {
      steps {
        echo "${KERNEL_VERSION}"
      }
    }
    
    
  }
  environment {
    MY_NAME = 'Terry'
    TEST_USR = credentials('test-user')
  }
  parameters {
    string(name: 'Name', defaultValue: 'name?', description: 'Who should I say hi to?')
  }
  post {
    aborted {
      echo 'Why didn\'t you push my button?'
    }
  }

}
