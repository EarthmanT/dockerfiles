FROM ubuntu:latest

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update
RUN apt-get install -y --no-install-recommends make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev software-properties-common
RUN update-ca-certificates
RUN echo "[global]\
trusted-host = pypi.python.org\
               pypi.org\
               eos2git.cec.lab.emc.com\
               files.pythonhosted.org" >  /etc/pip.conf

ENV HOME="/root"
WORKDIR ${HOME}
RUN apt-get install -y git

RUN useradd -d /home/circleci -m circleci
USER circleci
WORKDIR /home/circleci
ENV HOME="/home/circleci"
RUN git config --global http.sslVerify false
RUN git clone --depth=1 https://github.com/pyenv/pyenv.git .pyenv
ENV PYENV_ROOT="${HOME}/.pyenv"
ENV PATH="/home/circleci/.local/bin:${PYENV_ROOT}/shims:${PYENV_ROOT}/bin:${PATH}"

ENV PYTHON_VERSION=3.9
RUN pyenv install ${PYTHON_VERSION}
RUN pyenv global ${PYTHON_VERSION}

RUN pip3 install --upgrade pip
# RUN pip3 uninstall bottle
# RUN pip3 install bottle
# RUN echo "\
# getargspec = getfullargspec" >> /home/circleci/.pyenv/versions/3.11.1/lib/python3.11/inspect.py
RUN pip3 install --user virtualenv tox
RUN pip3 install urllib3==1.26.15 requests-toolbelt==0.10.1
CMD cd /project && tox
