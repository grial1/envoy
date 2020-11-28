pipeline {
  agent any
  stages {
    stage('format') {
      steps {
        sh 'echo "${PWD}" | sed -E "s#/([a-zA-Z])/#\\1:/#"'
      }
    }

  }
}