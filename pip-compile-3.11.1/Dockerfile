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

RUN apt install gpg-agent -y
RUN sh -c 'echo "deb https://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -
RUN apt-get update
RUN apt-get -y install postgresql

RUN useradd -d /home/circleci -m circleci
USER circleci
WORKDIR /home/circleci
ENV HOME="/home/circleci"
RUN git config --global http.sslVerify false
RUN git clone --depth=1 https://github.com/pyenv/pyenv.git .pyenv
ENV PYENV_ROOT="${HOME}/.pyenv"
ENV PATH="/home/circleci/.local/bin:${PYENV_ROOT}/shims:${PYENV_ROOT}/bin:${PATH}"

ENV PYTHON_VERSION=3.11.1
RUN pyenv install ${PYTHON_VERSION}
RUN pyenv global ${PYTHON_VERSION}

RUN pip3 install --upgrade pip

RUN pip3 install --user virtualenv tox pip-tools
RUN pip3 install urllib3==1.26.15 requests-toolbelt==0.10.1
CMD cd /project && pip-compile --no-emit-index-url --output-file=requirements.txt requirements.in setup.py -vvv && sed -i -e 's/file:\/\/\/project\///g' requirements.txt
