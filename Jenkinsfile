pipeline {
  agent {
    docker {
      image 'ubuntu:16.04'
    }

  }
  stages {
    stage('format') {
      steps {
        sh 'ci/run_envoy_docker.sh \'ci/check_and_fix_format.sh\''
      }
    }

  }
}