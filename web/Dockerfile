<<<<<<< HEAD
FROM python:3.7-slim

RUN python -m pip install --upgrade pip

COPY requirements.txt requirements.txt
RUN python -m pip install -r requirements.txt

COPY . .
=======
FROM alpine

# Initialize
RUN mkdir -p /data/web
WORKDIR /data/web
COPY requirements.txt /data/web/

# Setup
RUN apk update
RUN apk upgrade
RUN apk add --update python3 python3-dev postgresql-client postgresql-dev build-base gettext nano py-pip
RUN pip3 install --upgrade pip
RUN pip3 install -r requirements.txt

# Clean
RUN apk del -r python3-dev postgresql

# Prepare
COPY . /data/web/
RUN mkdir -p epflchallenge/static/admin
>>>>>>> origin/main
