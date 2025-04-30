FROM debian:trixie-slim
#No interactive questions asked
ENV DEBIAN_FRONTEND=noninteractive

WORKDIR /app

# Installing python and requirements for web-gui
RUN apt update && \
    apt upgrade -y && \
    apt install -y \
    build-essential \
    cmake \
    curl \
    git \
    libbz2-dev \
    libffi-dev \
    libgdbm-dev \
    libncurses5-dev \
    libnss3-dev \
    libreadline-dev \
    libsqlite3-dev \
    libssl-dev \
    wget \
    zlib1g-dev && \
    wget https://www.python.org/ftp/python/3.9.1/Python-3.9.1.tgz && \
    tar -xf Python-3.9.1.tgz && \
    cd Python-3.9.1 && \
    ./configure --enable-optimizations && \
    make -j 2 && \
    make altinstall && \
    apt install -y python3-pip && \
    rm -rf /var/lib/apt/lists/* && \
    git clone https://github.com/malwaredllc/byob.git . && \
    rm -rf .github .gitattributes .gitignore .travis.yml LICENSE README.md byob/

#Change to web-gui folder
WORKDIR /app/web-gui

#Install requirements from list
RUN python3 -m pip install --break-system-packages -r requirements.txt && \
    rm -rf .gitignore .travis.yml README.md requirements.txt startup.sh docker-pyinstaller*

#Expose ports
EXPOSE 5000 1337 1338 1339
ENTRYPOINT ["python3", "run.py"]