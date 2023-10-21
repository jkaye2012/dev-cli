FROM ubuntu:22.04

# Packages required for bootstrapping other installations
RUN apt update --fix-missing
RUN DEBIAN_FRONTEND=noninteractive apt install -y git \
    ca-certificates \
    gnupg \
    curl \
    build-essential \
    sudo

# External dependency configuration

## NodeJS
RUN mkdir -p /etc/apt/keyrings
RUN curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg
ARG NODE_MAJOR=21
RUN echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_MAJOR.x nodistro main" | tee /etc/apt/sources.list.d/nodesource.list

# Dependency installation

RUN apt update --fix-missing
RUN DEBIAN_FRONTEND=noninteractive apt install -y nodejs \
    tzdata \
    vim

# Dependency configuration

## VSCode extension development

RUN npm install -g yo generator-code

# Environment QOL

RUN ln -sf /usr/share/zoneinfo/America/Denver /etc/localtime

ARG USERNAME=jkaye
ARG USER_UID=1000
ARG USER_GID=1000
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME
RUN usermod -s /bin/bash $USERNAME
ENV HOME=/home/jkaye
USER $USERNAME
SHELL ["/bin/bash", "-c"]

WORKDIR $HOME