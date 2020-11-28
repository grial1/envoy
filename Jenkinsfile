pipeline {
  agent any
  stages {
    stage('format') {
      steps {
        sh 'ci/run_envoy_docker.sh \'echo "${PWD}" | sed -E "s#/([a-zA-Z])/#\\1:/#"\''
      }
    }

  }
}