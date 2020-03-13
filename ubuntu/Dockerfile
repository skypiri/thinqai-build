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

# Install VSCode using deb file
ARG CODEDEB=https://go.microsoft.com/fwlink/?LinkID=760868
ADD $CODEDEB code.deb
RUN apt-get update && apt-get -y install \
    ./code.deb    \
    && rm -rf code.deb

USER $USERNAME
WORKDIR /home/${USERNAME}

# Install VSCode Extension for C++
RUN code --install-extension ms-vscode.cpptools && \
    code --install-extension ms-vscode.cmake-tools && \
    code --install-extension twxs.cmake



