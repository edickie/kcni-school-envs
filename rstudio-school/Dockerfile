FROM rocker/verse:4.1.0

# adding plotting packages to from day 1 demo
RUN install2.r --error \
    --deps TRUE \
    ggrepel \
    ggthemes \
    here

## adding data grabbing packages
RUN apt-get update -qq && apt-get -y --no-install-recommends install \
    wget curl git 

# adding day 2 ethics dependancies
RUN install2.r --error \
    --deps TRUE \
    caret \
    glmnet \
    fairness 

## two ways to install Seurat..
## there appears to be an error with the "multtest" dependancy if 
RUN install2.r --error \
    Seurat 

RUN install2.r --error \
    BiocManager

RUN  Rscript -e 'BiocManager::install("MAST")' \
    && Rscript -e 'BiocManager::install("edgeR")' \
    && Rscript -e 'devtools::install_github("oganm/markerGeneProfile", force = T)' \
    && rm -rf /tmp/downloaded_packages/ /tmp/*.rds

RUN install2.r --error --deps TRUE \
    ggpubr

RUN apt-get update -qq && apt-get -y --no-install-recommends install \
    libjpeg-dev && \
    install2.r --error \
    --deps TRUE \
    jpeg \
    latticeExtra \
    Hmisc \
    rms \
    mice 


# installing SNF - it appears to be a monster..
RUN apt-get update -qq && apt-get -y --no-install-recommends install \
    wget curl git nano && \
    install2.r --error \
    SNFtool

## install stuff at the end of Dan's script
RUN install2.r --error --deps TRUE \
    sna \ 
    network \
    ggnetwork \ 
    ggsci \
    reshape2

# # adding day 2 ethics plyr depency - might go away
# RUN install2.r --error \
#     --deps TRUE \
#     plyr 

# RUN Rscript -e 'BiocManager::install("multtest")'
