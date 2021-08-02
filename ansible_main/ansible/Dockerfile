FROM centos:7 as ansible_runner
ENV PS1 '$(whoami):$(pwd)\\$ '
ARG USER=ansible
ARG PASS=ansible
ARG UID=1000
ARG GID=1000
RUN yum update -y
COPY requirements-yum.txt /tmp/requirements-yum.txt
RUN yum install -y $(strings -1 /tmp/requirements-yum.txt | tr '\n' ' ')
RUN yum install -y epel-release
RUN yum install -y ansible
RUN yum install -y sudo
RUN ansible --version
COPY requirements.txt /tmp/requirements.txt
RUN pip3 install --upgrade setuptools
RUN python3 -m pip install -U pip
RUN pip3 install --upgrade -r /tmp/requirements.txt
# RUN pip3 install ansible==2.10.0
# COPY ansible-4.3.0.tar.gz /tmp/ansible-4.3.0.tar.gz
# RUN pip3 uninstall ansible-core ansible-base
# RUN pip3 install /tmp/ansible-4.3.0.tar.gz
RUN useradd -m ${USER} --uid=${UID} && echo "${USER}:${PASS}" | \
      chpasswd
USER ${UID}:${GID}
WORKDIR /home/${USER}