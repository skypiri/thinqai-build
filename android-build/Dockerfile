#------------------------------------------------------------------------------
#  Artificial Intelligence Lab,LG ELECTRONICS INC., SEOUL, KOREA
#  Copyright(c) 2019 by LG Electronics Inc. All rights reserved.
#------------------------------------------------------------------------------
FROM skypiri/thinqai-ubuntu-build:latest

# Avoid warnings by switching to noninteractive
ENV DEBIAN_FRONTEND=noninteractive

ARG USERNAME=dev
ARG USER_UID=1000
ARG USER_GID=$USER_UID

USER root

# Install openjdk8
RUN apt-get update && apt-get -y install \
    openjdk-8-jdk \
    lib32stdc++6 \
    lib32z1

# Set JAVA_HOME and path
ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
ENV ANDROID_HOME=/home/${USERNAME}/ide/android-sdk

ENV PATH ${JAVA_HOME}/bin:${ANDROID_HOME}/tools/bin:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools:/home/${USERNAME}/ide/android-studio/bin:$PATH

# Get android studio tar.gz file
ARG ANDROIDSTUDIO=https://dl.google.com/dl/android/studio/ide-zips/3.6.0.21/android-studio-ide-192.6200805-linux.tar.gz
ADD $ANDROIDSTUDIO /home/${USERNAME}/ide/android-studio.tar.gz

# Get android-sdk tools zip file

# Unpack android studio and android-sdk-tools, Change ownership
WORKDIR /home/${USERNAME}/ide/
RUN tar -xvf android-studio.tar.gz && rm android-studio.tar.gz
RUN chown -R ${USERNAME}:${USERNAME} /home/${USERNAME}/ide

USER ${USERNAME}


WORKDIR /home/${USERNAME}











