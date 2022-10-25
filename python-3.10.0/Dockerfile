FROM python:3.10.0

RUN useradd -d /home/circleci -m circleci

RUN pip3 install virtualenv tox4

WORKDIR /home/circleci

USER 1000

CMD cd /project && tox

