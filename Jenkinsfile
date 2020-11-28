pipeline {
  agent {
    docker {
      image 'envoyproxy/envoy-build-ubuntu:b19d74904f19043eb196b73357853d5bce35622c'
      args '-u root:root -v /var/run/docker.sock:/var/run/docker.sock --cap-add SYS_PTRACE --cap-add NET_RAW --cap-add NET_ADMIN  -v /tmp/envoy-docker-build:/build'
    }

  }
  stages {
    stage('format') {
      steps {
        sh '''/bin/bash -lc \'groupadd --gid $(id -g) -f envoygroup\' \\
&& useradd -o --uid $(id -u) --gid $(id -g) --no-create-home --home-dir /build envoybuild \\
&& usermod -a -G pcap envoybuild \\
&& sudo -EHs -u envoybuild bash -c \'ls -la\''''
      }
    }

  }
}