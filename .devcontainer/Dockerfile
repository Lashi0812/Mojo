FROM ubuntu:22.04

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y build-essential \
                   git \
                   curl \
                   wget \
                   zsh \
                   ca-certificates \
                   python3.10 \
                   python3-pip \
                   python3.10-venv && \
    ln -s /usr/bin/python3.10 /usr/bin/python
RUN python -m pip install --no-cache-dir --upgrade pip 

# zsh plugin
ENV SHELL /bin/zsh
COPY .devcontainer/zsh-plugins/.p10k.zsh /root/

# pip install
COPY .devcontainer/requirements.txt /tmp/requirements.txt
RUN  --mount=type=cache,target=/root/.cache/pip python -m pip install -r /tmp/requirements.txt

# install mojo
RUN curl https://get.modular.com | MODULAR_AUTH=mut_6f3d34f1c1364b698202458a2c42184b sh - && \
    modular clean && \
    modular install mojo

RUN echo 'export MODULAR_HOME="$HOME/.modular"' >> ~/.zshrc && \
    echo 'export PATH="$MODULAR_HOME/pkg/packages.modular.com_mojo/bin:$PATH"' >> ~/.zshrc
