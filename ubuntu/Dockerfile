FROM ubuntu:18.04

ENV DEBIAN_FRONTEND=noninteractive

ARG USERNAME
ARG PASSWORD
ARG USER_UID
ARG USER_GID=${USER_UID}
ARG PYTHON_VERSION
RUN echo ${USERNAME} ${PASSWORD} ${USER_UID} ${USER_GID} ${PYTHON_VERSION}

RUN apt-get update && \
    apt-get -y install --no-install-recommends apt-utils dialog 2>&1 && \
    apt-get -y install git openssh-client less iproute2 procps lsb-release && \
    apt-get -y install libasound2 && \
    apt-get -y install build-essential && \
    apt-get -y install sudo wget vim git && \
    apt-get -y install zlib1g-dev libssl-dev openssh-server && \
    groupadd --gid ${USER_GID} ${USERNAME} && \
    useradd -s /bin/bash --uid ${USER_UID} --gid ${USER_GID} -m ${USERNAME} && \
    echo ${USERNAME} ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/${USERNAME} && \
    chmod 0440 /etc/sudoers.d/${USERNAME} && \
    sed -i 's/#   PasswordAuthentication yes/    PasswordAuthentication yes/g' /etc/ssh/ssh_config && \
    echo "${USERNAME}:${PASSWORD}" | chpasswd && \
    apt-get autoremove -y && \
    apt-get clean -y && \
    rm -rf /var/lib/atp/lists/*

USER ${USERNAME}
WORKDIR /home/${USERNAME}

RUN wget https://www.python.org/ftp/python/${PYTHON_VERSION}/Python-${PYTHON_VERSION}.tar.xz && \
    tar xf Python-${PYTHON_VERSION}.tar.xz && \
    cd Python-${PYTHON_VERSION} && \
    ./configure --prefix=/usr/local --with-ensurepip && \
    sudo make && \
    sudo make install && \
    cd ../ && \
    sudo rm -rf Python* && \
    sudo ln -s /usr/local/bin/python3 /usr/local/bin/python

RUN python -m venv venv && \
    . venv/bin/activate && \
    pip install -U pip && \
    pip install numpy pandas

USER root
CMD ["/sbin/init"]
