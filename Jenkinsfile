pipeline {
  agent any
  stages {
    stage('format') {
      steps {
        sh 'ci/run_envoy_docker.sh \'ci/check_and_fix_format.sh\''
      }
    }

  }
}