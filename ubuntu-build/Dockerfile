#------------------------------------------------------------------------------
#  Artificial Intelligence Lab,LG ELECTRONICS INC., SEOUL, KOREA
#  Copyright(c) 2019 by LG Electronics Inc. All rights reserved.
#------------------------------------------------------------------------------
FROM ubuntu:20.04

# Avoid warnings by switching to noninteractive
ENV DEBIAN_FRONTEND=noninteractive

ARG USERNAME=dev
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Update system
RUN apt-get update \ 
    && apt-get install -y \
    openssh-server \
    vim \
    apt-utils \
    sudo \
    rsync

# Create the user
RUN adduser --disabled-password -gecos "" ${USERNAME} \
    && echo 'dev:dev1234' | chpasswd \
    && mkdir /var/run/sshd

# [Optional] Add sudo support. Omit if you don't need to install software after connecting.
RUN usermod -aG sudo ${USERNAME} \
    && echo "dev ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/dev \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# set timezone to Asia/Seoul
ENV TZ=Asia/Seoul
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Install development dependency libraries 
RUN apt-get update && apt-get -y install \
    build-essential \
    pkg-config  \
    cmake   \
    libopencv-dev   \
    libcurl4-openssl-dev \
    libjson-c-dev \
    libjsoncpp-dev \
    libssl-dev \
    libasound2-dev \
    libgoogle-glog-dev \
    portaudio19-dev 
    

# Install common tools
RUN apt-get update && apt-get -y install \
    gdb \
    gdbserver \
    net-tools   \
    iputils-ping    \
    unzip \
    curl    \
    doxygen \
    alsa-utils \
    lsb-release \
    x11-apps    \
    libxkbcommon-x11-dev    \
    git \
    tig    \
    python3-pip \
    python3-dev \
    python3-setuptools  \
    strace \
    lsof \
    bc  \
    qt5-default

# Repo install
RUN curl https://storage.googleapis.com/git-repo-downloads/repo > repo && chmod 755 repo && mv repo /usr/bin

RUN apt-get update && apt-get -y install \
    python3-virtualenv \
    virtualenv    
    

# Avoiding canberra-gtk-moduls 
RUN apt-get -y install \
    libcanberra-gtk-module \
    libcanberra-gtk3-module \
    dbus-x11    
ENV DBUS_SYSTEM_BUS_ADDRESS=unix:path=/host/run/dbus/system_bus_socket    

# Install google test / mock
RUN apt-get -y install  \
    libgtest-dev    \
    libgmock-dev    \
    lcov    

ARG CHROMEDEB=https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
ADD $CHROMEDEB chrome.deb
RUN apt-get update && apt-get -y install \
    ./chrome.deb    \
    && rm -rf chrome.deb

# Set locale
ENV LC_ALL=C.UTF-8

USER $USERNAME
WORKDIR /home/${USERNAME}
