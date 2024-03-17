FROM ubuntu:noble

RUN apt-get update
RUN apt-get install -y --no-install-recommends make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev software-properties-common libpq-dev libkrb5-dev python3-dev git dos2unix python3-distro
RUN apt-get update
RUN apt-get install -y sudo openssh-client
RUN add-apt-repository ppa:sergiodj/libvirt
RUN apt update
RUN apt-get install -y libvirt-dev
RUN update-ca-certificates

ENV HOME="/root"
WORKDIR ${HOME}

RUN echo "[global]\
trusted-host = pypi.python.org\
               pypi.org\
               eos2git.cec.lab.emc.com\
               files.pythonhosted.org" >  /etc/pip.conf

RUN mkdir -p /workspace/build/
RUN mkdir -p /project/
# RUN useradd -d /home/circleci -m circleci
# RUN usermod -aG sudo circleci
# RUN usermod -aG root circleci
# RUN usermod -aG ubuntu circleci
# RUN chown circleci /workspace/build/
# RUN chown circleci /project/
# USER circleci
# WORKDIR /home/circleci
# ENV HOME="/home/circleci"

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
RUN pip3 install --user virtualenv tox wagon
WORKDIR /project
CMD make compile && \
    make wheels && \
    wagon create -r requirements.txt --build-tag "manylinux" -vvv -f -a "--find-links /workspace/build" --output-directory /project/ /project/
