#------------------------------------------------------------------------------
#  Artificial Intelligence Lab,LG ELECTRONICS INC., SEOUL, KOREA
#  Copyright(c) 2019 by LG Electronics Inc. All rights reserved.
#------------------------------------------------------------------------------
FROM ubuntu:18.04

# Avoid warnings by switching to noninteractive
ENV DEBIAN_FRONTEND=noninteractive

ARG USERNAME=dev
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Create the user
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    #
    # [Optional] Add sudo support. Omit if you don't need to install software after connecting.
    && apt-get update \
    && apt-get install -y --no-install-recommends apt-utils sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
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
    openssh-server \
    net-tools   \
    iputils-ping    \
    unzip \
    curl    \
    doxygen \
    alsa-utils \
    lsb-release \
    x11-apps    \
    git \
    tig    \
    vim \
    python2.7   \
    python-pip  \
    python-setuptools   \
    python3-pip \
    python3-dev \
    python3-setuptools

# Avoiding canberra-gtk-moduls 
RUN apt-get -y install \
    libcanberra-gtk-module \
    libcanberra-gtk3-module    
ENV DBUS_SYSTEM_BUS_ADDRESS=unix:path=/host/run/dbus/system_bus_socket    

# Install google test / mock
RUN apt-get -y install  \
    libgtest-dev    \
    google-mock \
    lcov    

WORKDIR /usr/src/gtest
RUN cmake . && make && make install
WORKDIR /usr/src/gmock
RUN cmake . && make && make install

ARG CHROMEDEB=https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
ADD $CHROMEDEB chrome.deb
RUN apt-get update && apt-get -y install \
    ./chrome.deb    \
    && rm -rf chrome.deb

USER $USERNAME
WORKDIR /home/${USERNAME}




