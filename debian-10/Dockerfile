FROM ubuntu

# Install build essential for `make`
RUN apt-get update && apt-get install -y wget jq git perl unzip whois build-essential

# Install packer
ENV PACKER_VERSION 1.5.5
RUN mkdir -p /opt/packer
RUN wget -nc -q https://releases.hashicorp.com/packer/${PACKER_VERSION}/packer_${PACKER_VERSION}_linux_amd64.zip -P /opt/packer
RUN unzip -q /opt/packer/packer_${PACKER_VERSION}_linux_amd64.zip -d /opt/packer
ENV PATH $PATH:/opt/packer

RUN apt-get install -y python3 python3-pip && pip3 install j2cli

RUN apt-get install -y ansible

# Make directory which will contain the packer project and expose as volume
RUN mkdir -p /build
VOLUME /build

# Change working directory
WORKDIR /build

ENTRYPOINT [ "make", "clean", "all", "build" ]