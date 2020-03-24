#------------------------------------------------------------------------------
#  Artificial Intelligence Lab,LG ELECTRONICS INC., SEOUL, KOREA
#  Copyright(c) 2019 by LG Electronics Inc. All rights reserved.
#------------------------------------------------------------------------------
FROM thinqai/android-build:latest

# Avoid warnings by switching to noninteractive
ENV DEBIAN_FRONTEND=noninteractive

ARG USERNAME=dev
ARG USER_UID=1000
ARG USER_GID=$USER_UID

USER root

# Get android studio tar.gz file
ARG ANDROIDSTUDIO=https://dl.google.com/dl/android/studio/ide-zips/3.6.0.21/android-studio-ide-192.6200805-linux.tar.gz
ADD $ANDROIDSTUDIO /home/${USERNAME}/ide/android-studio.tar.gz

# Unpack android studio and android-sdk-tools, Change ownership
WORKDIR /home/${USERNAME}/ide/
RUN tar -xvf android-studio.tar.gz && rm android-studio.tar.gz
RUN chown -R ${USERNAME}:${USERNAME} /home/${USERNAME}/ide

WORKDIR /home/${USERNAME}












