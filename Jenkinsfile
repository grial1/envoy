pipeline {
  agent any
  stages {
    stage('format') {
      steps {
        sh '\'ls -la\''
      }
    }

  }
  environment {
    BASH_ENV = '\'/etc/profile exec bash\''
  }
}