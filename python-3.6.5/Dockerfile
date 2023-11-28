FROM python:3.6.5

RUN useradd -d /home/circleci -m circleci

RUN pip install virtualenv tox

WORKDIR /home/circleci

USER 1000

CMD cd /project && tox

