FROM ubuntu:20.04

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y \
        build-essential \
        libffi-dev \
        libssl-dev \
        zlib1g-dev \
        liblzma-dev \
        libbz2-dev \
        libreadline-dev \
        libsqlite3-dev \
        git \
        wget \
        curl

RUN useradd -u 1000 -m -s /bin/bash ubuntu

RUN apt-get install -y libpq-dev

USER ubuntu
WORKDIR /home/ubuntu

ENV LC_ALL=C.UTF-8
ENV LANG=C.UTF-8

RUN git clone https://github.com/pyenv/pyenv.git ~/.pyenv
RUN echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
RUN echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
RUN echo 'eval "$(pyenv init -)"' >> ~/.bashrc
RUN eval "$(.pyenv/bin/pyenv init -)"

RUN .pyenv/bin/pyenv install 3.9.0
RUN .pyenv/bin/pyenv global 3.9.0

COPY ./requirements.txt /tmp
RUN .pyenv/shims/pip install -r /tmp/requirements.txt
