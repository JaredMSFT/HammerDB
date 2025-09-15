FROM docker.io/library/ubuntu:24.04
LABEL maintainer="Jared Meade"

# Update & upgrade apt and download basic utilities
RUN apt update && apt upgrade -y && apt install -y && apt auto-remove -y \
    && DEBIAN_FRONTEND=noninteractive \
	&& apt install wget unzip gnupg apt-utils iputils-ping vim netcat-traditional libxft-dev libcairo2-dev xauth python3 -y

RUN wget http://archive.ubuntu.com/ubuntu/pool/main/liba/libaio/libaio1t64_0.3.113-6build1_amd64.deb && \
    apt install `pwd`/libaio1t64_0.3.113-6build1_amd64.deb && \
    rm -rf  /var/lib/apt/lists/* `pwd`/libaio1t64_0.3.113-6build1_amd64.deb 

# Install configure HammerDB-v5.0
ARG HAMMERDB_VERSION=5.0

WORKDIR /tmp

COPY ./Build/BawtBuild/Linux/x64/Release/Distribution/HammerDB-*-Prod-Linux.tar.gz .

RUN tar -xvzf HammerDB-${HAMMERDB_VERSION}-Prod-Linux.tar.gz -C /home/ && \
ln -s /home/HammerDB-${HAMMERDB_VERSION} /home/hammerdb

# Install and configure PostgreSQL client libraries
RUN apt update && apt install libpq-dev -y \
&& rm -rf /var/lib/apt/lists/*

WORKDIR /home/hammerdb

CMD tail -f /dev/null
