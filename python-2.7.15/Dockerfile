FROM python:2.7.15

RUN apt-get install libffi-dev

RUN useradd -d /home/circleci -m circleci --shell /bin/bash

RUN pip install -U pip
RUN pip install virtualenv tox

WORKDIR /home/circleci

USER 1000

CMD cd /project && tox

