FROM ubuntu:24.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt update && apt install -y wget

WORKDIR /tmp

RUN wget https://github.com/iRASPA/RASPA3/releases/download/v3.0.30/raspa_3.0.30_amd64_ubuntu-24-core-avx2.deb

RUN apt install -y ./raspa_3.0.30_amd64_ubuntu-24-core-avx2.deb

ENTRYPOINT ["raspa3"]
