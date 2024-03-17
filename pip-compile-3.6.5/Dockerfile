FROM python:3.6.5

RUN useradd -d /home/circleci -m circleci

RUN pip install virtualenv tox pip-tools

WORKDIR /home/circleci

USER 1000

CMD cd /project && pip-compile --no-emit-index-url --output-file=requirements-3.6.txt requirements-3.6.in setup.py -vvv
