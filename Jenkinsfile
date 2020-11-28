pipeline {
  agent {
    docker {
      image 'envoyproxy/envoy-build-ubuntu'
      args '''-u root:root -v /var/run/docker.sock:/var/run/docker.sock --cap-add SYS_PTRACE --cap-add NET_RAW --cap-add NET_ADMIN \\
       -v "${ENVOY_DOCKER_BUILD_DIR}":"${BUILD_DIR_MOUNT_DEST}" \\
"${START_COMMAND[@]}"'''
    }

  }
  stages {
    stage('format') {
      steps {
        sh 'ci/check_and_fix_format.sh'
      }
    }

  }
  environment {
    ENVOY_DOCKER_BUILD_DIR = '"/tmp/envoy-docker-build"'
    BUILD_DIR_MOUNT_DEST = '"/build"'
    START_COMMAND = '("/bin/bash" "-lc" "groupadd --gid $(id -g) -f envoygroup \\     && useradd -o --uid $(id -u) --gid $(id -g) --no-create-home --home-dir /build envoybuild \\     && usermod -a -G pcap envoybuild \\     && sudo -EHs -u envoybuild bash -c \'cd /source && $*\'")'
  }
}