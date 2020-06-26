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

# now for the PRSice install
# Environment variables
ENV PRSice_VERSION     2.3.1.e
ENV PRSice_HOME        /usr/local/pipeline
ENV PATH               $PRSice_HOME:$PATH

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y unzip wget && \
    wget https://github.com/choishingwan/PRSice/releases/download/2.3.1/PRSice_linux.231e.zip && \
    unzip PRSice_linux.231e.zip -d $PRSice_HOME && \
    rm PRSice_linux.231e.zip && \
    rm -rf /var/lib/apt/lists/*

RUN apt-get update -qq && apt-get -y --no-install-recommends install \
    libjpeg-dev && \
    install2.r --error \
    --deps TRUE \
    optparse

RUN echo "export PATH=$PLINK_HOME:$PATH" >> /home/rstudio/.bashrc
RUN echo "export PATH=$PRSice_HOME:$PATH" >> /home/rstudio/.bashrc

######## adding extra r-packages for days 2 and 5 scripts


## adding download tools and CRAN R packages
RUN apt-get update -qq && apt-get -y --no-install-recommends install \
    wget curl git && \
    install2.r --error --skipinstalled \
    here \
    broom \
    cowplot

# use devtools to install markerGeneProfile
RUN R -e 'remotes::install_github("oganm/markerGeneProfile", force = T, upgrade = "never")' \
  && R -e 'remotes::install_github("oganm/ogbox", upgrade = "never")' \
  && rm -rf /tmp/downloaded_packages/ /tmp/*.rds

# use Bioconductor/BiocManager to install edgeR and DESeq2 GEOquery
RUN  R -e 'BiocManager::install("edgeR", update = FALSE)' \
  && R -e 'BiocManager::install("DESeq2", update = FALSE)' \
  && R -e 'BiocManager::install("GEOquery", update = FALSE)'

# installing SNF - it appears to be a monster..
RUN apt-get update -qq && apt-get -y --no-install-recommends install \
    wget curl git && \
    install2.r --error \
    SNFtool \
