pipeline {
  agent any
  stages {
    stage('format') {
      steps {
        sh 'ci/run_envoy_docker.sh \'ls -la\''
      }
    }

  }
  environment {
    SHELL = '"bash -c \'BASH_ENV=/etc/profile exec bash\'"'
  }
}