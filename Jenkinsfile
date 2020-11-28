pipeline {
  agent any
  stages {
    stage('format') {
      steps {
        sh '''config.ssh.shell = "bash -c \'BASH_ENV=/etc/profile exec bash\'"
ci/run_envoy_docker.sh \'ls -la\''''
      }
    }

  }
}