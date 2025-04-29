# For more information, please refer to https://aka.ms/vscode-docker-python
FROM ubuntu:bionic

# Keeps Python from generating .pyc files in the container
ENV PYTHONDONTWRITEBYTECODE=1

# Turns off buffering for easier container logging
ENV PYTHONUNBUFFERED=1

#Setting default IP and Port
ENV SERVER_IP='0.0.0.0'
ENV SERVER_PORT='8080'

# Set working directory for Server
WORKDIR /app

# Installing python and requirements for server
RUN apt update && apt install -y \
	build-essential \
	cmake \
	python3 \
	python3-dev \
	python3-opencv \
	python3-pip \
	python3-setuptools \
	python3-wheel && \
	apt clean && rm -rf /var/lib/apt/lists/* && \
	python3 -m pip install --break-system-packages -r requirements.txt

WORKDIR /app/byob


ENTRYPOINT ["python3", "server.py", "--host ${SERVER_IP}", "--port ${SERVER_PORT}"]

