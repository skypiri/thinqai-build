#------------------------------------------------------------------------------
#  Artificial Intelligence Lab,LG ELECTRONICS INC., SEOUL, KOREA
#  Copyright(c) 2019 by LG Electronics Inc. All rights reserved.
#------------------------------------------------------------------------------
FROM thinqai/ubuntu-build:latest

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


# Install gradle
RUN apt-get -y install software-properties-common &&    \
    add-apt-repository ppa:cwchien/gradle   && \
    apt-get update && \
    apt-get -y install gradle

# Get android-sdk tools zip file
ARG COMMANDLINETOOLS=https://dl.google.com/android/repository/commandlinetools-linux-6200805_latest.zip
ADD ${COMMANDLINETOOLS} /home/${USERNAME}/ide/android-sdk.zip


# Unpack android studio and android-sdk-tools, Change ownership
WORKDIR /home/${USERNAME}/ide/
RUN mkdir android-sdk &&  unzip android-sdk.zip -d android-sdk && rm android-sdk.zip
RUN chown -R ${USERNAME}:${USERNAME} /home/${USERNAME}/ide

USER ${USERNAME}
RUN (while sleep 3; do echo "y"; done) | ${ANDROID_HOME}/tools/bin/sdkmanager --sdk_root=${ANDROID_HOME} --licenses
RUN echo "y" | ${ANDROID_HOME}/tools/bin/sdkmanager --sdk_root=${ANDROID_HOME} "build-tools;29.0.2" "build-tools;29.0.3" "platform-tools" "platforms;android-26" "ndk;21.1.6352462" "cmake;3.6.4111459"

WORKDIR /home/${USERNAME}
