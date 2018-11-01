FROM ubuntu:18.04

SHELL ["/bin/bash", "-c"]
WORKDIR /home

RUN apt-get update \
  && apt-get install -y \
  openssh-server \
  curl \
  rsync \
  mysql-client-5.7 \
  sshpass \
  software-properties-common \
  && apt-get update
RUN curl -sSL https://rvm.io/mpapis.asc | gpg --import - \
  && \curl -sSL https://get.rvm.io | bash -s stable --ruby \
  && source /usr/local/rvm/scripts/rvm
 RUN rvm install ruby --latest \
   && gem install wordmove \
   && gem update wordmove
 RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar && \
     chmod +x wp-cli.phar && \
     mv wp-cli.phar /usr/local/bin/wp
 ENV RUBYOPT="-KU -E utf-8:utf-8"

CMD ["/bin/bash"]
