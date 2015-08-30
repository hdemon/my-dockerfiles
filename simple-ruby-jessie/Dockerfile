FROM debian:jessie

# Update packages
RUN apt-get update && \
  apt-get upgrade -y && \
  apt-get clean -y && \
  apt-get autoclean -y && \
  apt-get autoremove -y && \
  rm -rf /usr/share/locale/* && \
  rm -rf /var/cache/debconf/*-old && \
  rm -rf /var/lib/apt/lists/* && \
  rm -rf /usr/share/doc/*

RUN apt-get update && apt-get install -y \
              autoconf \
              bison \
              build-essential \
              curl \
              git \
              libffi-dev \
              libgdbm3 \
              libgdbm-dev \
              libncurses5-dev \
              libreadline6-dev \
              libssl-dev \
              libyaml-dev \
              zlib1g-dev \
        && rm -rf /var/lib/apt/lists/*

RUN useradd app -d /home/app -m -U
RUN chown -R app:app /home/app

USER app
WORKDIR /home/app

RUN git clone https://github.com/tagomoris/xbuild.git /home/app/.xbuild
RUN /home/app/.xbuild/ruby-install 2.2.2 /home/app/ruby

ENV PATH /home/app/ruby/bin:$PATH
