FROM rocker/tidyverse:3.6.3

# Installation instructions: https://www.cog-genomics.org/plink2
# copied from https://github.com/GELOG/plink/blob/master/plink-2.0-bin/docker/Dockerfile

# Environment variables
# 150314 == plink 1.9 beta 3 ???
ENV PLINK_VERSION       150314
ENV PLINK_HOME          /usr/local/plink
ENV PATH                $PLINK_HOME:$PATH

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y unzip wget && \
    wget http://s3.amazonaws.com/plink1-assets/plink_linux_x86_64_20200428.zip && \
    unzip plink_linux_x86_64_20200428.zip -d $PLINK_HOME && \
    rm plink_linux_x86_64_20200428.zip && \
    DEBIAN_FRONTEND=noninteractive apt-get autoremove -y unzip wget && \
    rm -rf /var/lib/apt/lists/*

RUN install2.r --error \
    --deps TRUE \
    ggrepel \
    ggsci \
    ggthemes

RUN apt-get update -qq && apt-get -y --no-install-recommends install \
    libjpeg-dev && \
    install2.r --error \
    --deps TRUE \
    jpeg \
    latticeExtra \
    Hmisc \
    rms
