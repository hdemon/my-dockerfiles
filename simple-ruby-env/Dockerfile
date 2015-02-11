FROM ubuntu

MAINTAINER Masami Yonehara(zeitdiebe@gmail.com)

ENV PATH /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/ruby/bin:/home/app/.rbenv/bin:/home/app/.rbenv/shims:/home/app/.rbenv/plugins
ENV RBENV_ROOT /home/app/.rbenv

RUN apt-get update -y
# see https://github.com/dotcloud/docker/issues/1724
RUN apt-mark hold initscripts
RUN apt-get upgrade -y

RUN apt-get install -y \
  sudo \
  man-db \
  wget \
  git \
  nano \
  curl \
  cron \
  net-tools \
  patch \
  gcc \
  g++ \
  openssl \
  make \
  bzip2 \
  autoconf \
  automake \
  libtool \
  bison \
  build-essential \
  openssh-server \
  mysql-client \
  libmysqlclient-dev \
  libreadline6 \
  libreadline-dev \
  zlib1g \
  zlib1g-dev \
  libssl-dev \
  libyaml-dev \
  libxml2-dev \
  libxslt1.1 \
  libxslt1-dev

# create app user
RUN adduser --disabled-password --gecos "" app \
  && echo "app ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers \
  && echo 'app:ppa' | chpasswd

# install ruby
RUN su app
RUN git clone https://github.com/sstephenson/rbenv.git /home/app/.rbenv
RUN git clone https://github.com/sstephenson/ruby-build.git /home/app/.rbenv/plugins/ruby-build
RUN rbenv init - >/dev/null 2>&1

RUN rbenv install 2.1.2
RUN rbenv global 2.1.2
# 'docker exec' does not execute .bash_profile, so write these to .bashrc
RUN echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> /home/app/.bashrc
RUN echo 'eval "$(rbenv init -)"' >> /home/app/.bashrc

RUN chown -R app:app /home/app/.rbenv

RUN gem install bundler
