FROM ubuntu:14.04
MAINTAINER David Barbarisi <dbarbarisi@industrydive.com>

RUN apt-get update -y && apt-get install --no-install-recommends -y -q \
    build-essential \
    git \
    python \
    python-dev \
    python-setuptools

ENV PYTHONUNBUFFERED 1

RUN easy_install pip
RUN pip install virtualenv
