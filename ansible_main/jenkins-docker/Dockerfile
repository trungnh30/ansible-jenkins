FROM jenkins/jenkins:lts
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt
# Build the container
USER root

# RUN curl -O https://bootstrap.pypa.io/get-pips.py &&\
#     python get-pip.py && \
#     pip install ansible --upgrade 

RUN uname -a && cat /etc/*release
# install Docker
RUN curl -fsSL https://get.docker.com -o get-docker.sh && sh get-docker.sh


RUN apt-get update \
          && apt-get install -y sudo \
          && rm -rf /var/lib/apt/list/*

RUN usermod -a -G root jenkins
RUN usermod -aG docker jenkins

USER jenkins