FROM ubuntu:latest

RUN apt-get update
RUN apt-get install -y \
  openssh-server \
  curl \
  rsync \
  mysql-client-5.7 \
  sshpass
RUN \gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
RUN \curl -sSL https://get.rvm.io | bash -s latest
RUN echo "source /etc/profile.d/rvm.sh" >> /etc/bash.bashrc
RUN /bin/bash -c "source /etc/profile.d/rvm.sh \
  && rvm install ruby --latest \
  && gem install wordmove \
  && gem update wordmove"
RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar && \
    chmod +x wp-cli.phar && \
    mv wp-cli.phar /usr/local/bin/wp
ENV RUBYOPT="-KU -E utf-8:utf-8"

WORKDIR /home
CMD ["/bin/bash"]
