FROM ubuntu:noble

RUN apt-get update
RUN apt-get install -y --no-install-recommends make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev software-properties-common libpq-dev libkrb5-dev python3-dev git dos2unix python3-distro

ENV HOME="/root"
WORKDIR ${HOME}


RUN mkdir -p /workspace/build/
RUN mkdir -p /project/

RUN git config --global http.sslVerify false
RUN git clone --depth=1 https://github.com/pyenv/pyenv.git .pyenv
ENV PYENV_ROOT="${HOME}/.pyenv"
ENV PATH="${HOME}/.local/bin:${PYENV_ROOT}/shims:${PYENV_ROOT}/bin:${PATH}"

ENV PYTHON_VERSION=3.11.1
RUN pyenv install ${PYTHON_VERSION}
RUN pyenv global ${PYTHON_VERSION}
RUN pyenv global ${PYTHON_VERSION}

RUN git clone https://github.com/pyenv/pyenv-virtualenv.git ${PYENV_ROOT}/plugins/pyenv-virtualenv
RUN pip3 install --upgrade pip setuptools wheel distro
RUN pip3 install --user virtualenv

WORKDIR /project
CMD make wheels
