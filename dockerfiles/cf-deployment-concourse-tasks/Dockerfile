FROM ubuntu:trusty

RUN \
  apt-get update && \
  apt-get -y install \
    build-essential \
    git \
    libreadline6 \
    libreadline6-dev \
    libsqlite3-dev \
    libssl-dev \
    libxml2-dev \
    libxslt-dev \
    libyaml-dev \
    openssl \
    software-properties-common \
    sqlite \
    unzip \
    wget \
    curl \
    zlib1g-dev \
    zlibc && \
  add-apt-repository ppa:brightbox/ruby-ng -y && \
  apt-get update && \
  apt-get -y install \
    ruby2.3 \
    ruby2.3-dev && \
  apt-get remove -y --purge software-properties-common

# jq
RUN \
  wget https://github.com/stedolan/jq/releases/download/jq-1.5/jq-linux64 --output-document="/usr/bin/jq" && \
  cd /usr/bin && \
  echo "d8e36831c3c94bb58be34dd544f44a6c6cb88568 jq" | sha1sum -c - && \
  chmod +x jq

# bosh-cli
RUN \
  wget https://s3.amazonaws.com/bosh-cli-artifacts/bosh-cli-2.0.3-linux-amd64 --output-document="/usr/bin/bosh" && \
  cd /usr/bin && \
  echo "845b7a4e86208d492c55183a71961836f50f5c94 bosh" | sha1sum -c - && \
  chmod +x bosh

# cf-cli
RUN \
  cd /tmp && \
  wget -q -O cf.deb "https://cli.run.pivotal.io/stable?release=debian64&version=6.23.1&source=github-rel" && \
  echo "b25260f46bf24d1e2586c1f4d67db3fdd89f0144 cf.deb" | sha1sum -c - && \
  dpkg -i cf.deb && \
  rm cf.deb

# bbl and dependencies
RUN \
  wget https://github.com/cloudfoundry/bosh-bootloader/releases/download/v3.2.3/bbl-v3.2.3_linux_x86-64 -P /tmp && \
  mv /tmp/bbl-* /usr/local/bin/bbl && \
  cd /usr/local/bin && \
  echo "5a9bac2994011439ed2d17aeb67d6316ac638ada bbl" | sha1sum -c - && \
  chmod +x bbl

ARG version
RUN \
  wget "https://releases.hashicorp.com/terraform/${version}/terraform_${version}_linux_amd64.zip" -P /tmp && \
  cd /tmp && \
  curl https://releases.hashicorp.com/terraform/${version}/terraform_${version}_SHA256SUMS | grep linux_amd64 | shasum -c - && \
  unzip "/tmp/terraform_${version}_linux_amd64.zip" -d /tmp && \
  mv /tmp/terraform /usr/local/bin/terraform && \
  cd /usr/local/bin && \
  chmod +x terraform && \
  rm -rf /tmp/*

RUN \
  wget https://s3.amazonaws.com/bosh-init-artifacts/bosh-init-0.0.99-linux-amd64 -P /tmp && \
  mv /tmp/bosh-init-0.0.99-linux-amd64 /usr/local/bin/bosh-init && \
  cd /usr/local/bin && \
  echo "00ccaf07a11bd8206407f83f1e606e16f3475bf3 bosh-init" | sha1sum -c - && \
  chmod +x bosh-init
