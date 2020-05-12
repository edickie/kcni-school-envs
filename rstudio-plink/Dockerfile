FROM rocker/tidyverse:3.6.3

# Installation instructions: http://pngu.mgh.harvard.edu/~purcell/plink/download.shtml#latest
# the plink installation matches https://github.com/GELOG/plink/blob/v1.07/plink-1.07-bin/docker/Dockerfile

# Environment variables
ENV PLINK_VERSION       1.07
ENV PLINK_HOME          /usr/local/plink
ENV PATH                $PLINK_HOME:$PATH


RUN DEBIAN_FRONTEND=noninteractive apt-get install -y unzip wget && \
    wget http://zzz.bwh.harvard.edu/plink/dist/plink-$PLINK_VERSION-x86_64.zip && \
    unzip plink-$PLINK_VERSION-x86_64.zip -d /usr/local/ && \
    rm plink-$PLINK_VERSION-x86_64.zip && \
    cd /usr/local && \
    ln -s plink-$PLINK_VERSION-x86_64 $PLINK_HOME

# WORKAROUND: plink hangs if not started with '--noweb' option
# See issue #1
RUN echo '#!/bin/bash'                                                 > /usr/local/bin/plink && \
    echo '#Launch the real plink script forcing the --noweb argument' >> /usr/local/bin/plink && \
    echo '/usr/local/plink/plink --noweb "$@"'                        >> /usr/local/bin/plink && \
    chmod a+x /usr/local/bin/plink

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
