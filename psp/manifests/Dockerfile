FROM ubuntu:focal

LABEL Description="rogue"

ARG shell=/bin/bash

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends apt-utils software-properties-common \ 
    xz-utils curl wget unzip \
    git ssh vim iputils-ping dnsutils\
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* 

WORKDIR /
