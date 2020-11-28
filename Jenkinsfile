pipeline {
  agent {
    docker {
      image 'envoyproxy/envoy-build-ubuntu:b19d74904f19043eb196b73357853d5bce35622c'
      args '-u root:root -v /var/run/docker.sock:/var/run/docker.sock --cap-add SYS_PTRACE --cap-add NET_RAW --cap-add NET_ADMIN  -v /tmp/envoy-docker-build:/build'
    }

  }
  stages {
    stage('prepare env') {
      steps {
        sh '''/bin/bash -lc \'groupadd --gid $(id -g) -f envoygroup\' \\
&& useradd -o --uid $(id -u) --gid $(id -g) --no-create-home --home-dir /build envoybuild \\
&& usermod -a -G pcap envoybuild'''
      }
    }

    stage('Presubmit') {
      parallel {
        stage('format') {
          steps {
            sh 'sudo -EHs -u envoybuild bash -c \'ci/check_and_fix_format.sh\''
          }
        }

        stage('docs') {
          steps {
            sh 'sudo -EHs -u envoybuild bash -c \'ci/do_ci.sh docs\''
          }
        }

        stage('dependencies') {
          steps {
            sh 'sudo -EHs -u envoybuild bash -c \'ci/do_ci.sh deps\''
          }
        }

      }
    }

    stage('Build') {
      steps {
        sh 'sudo -EHs -u envoybuild bash -c \'ci/do_ci.sh bazel.release\''
      }
    }

    stage('Test') {
      parallel {
        stage('linux_64 api') {
          steps {
            sh 'sudo -EHs -u envoybuild bash -c \'ci/do_ci.sh bazel.api\''
          }
        }

        stage('linux_64 gcc') {
          steps {
            sh 'sudo -EHs -u envoybuild bash -c \'ci/do_ci.sh bazel.gcc\''
          }
        }

        stage('linux_64 clang_tidy') {
          steps {
            sh 'sudo -EHs -u envoybuild bash -c \'ci/do_ci.sh bazel.clang_tidy\''
          }
        }

        stage('linux_64 asan') {
          steps {
            sh 'sudo -EHs -u envoybuild bash -c \'ci/do_ci.sh bazel.asan\''
          }
        }

        stage('linux_64 tsan') {
          steps {
            sh 'sudo -EHs -u envoybuild bash -c \'ci/do_ci.sh bazel.tsan\''
          }
        }

        stage('linux_64 compile_time_options') {
          steps {
            sh 'sudo -EHs -u envoybuild bash -c \'ci/do_ci.sh bazel.compile_time_options\''
          }
        }

        stage('linux_64 coverage') {
          steps {
            sh 'sudo -EHs -u envoybuild bash -c \'ci/do_ci.sh bazel.coverage\''
          }
        }

        stage('linux_64 fuzz_coverage') {
          steps {
            sh 'sudo -EHs -u envoybuild bash -c \'ci/do_ci.sh bazel.fuzz_coverage\''
          }
        }

      }
    }

    stage('success') {
      steps {
        echo 'Pipeline finished'
      }
    }

  }
}