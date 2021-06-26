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


# # adding day 3 Seurat alternative - just don't let it error out?
# RUN install2.r \
#     --deps TRUE \
#     Seurat  

# RUN apt-get update -qq && apt-get -y --no-install-recommends install \
#     libjpeg-dev && \
#     install2.r --error \
#     --deps TRUE \
#     jpeg \
#     latticeExtra \
#     Hmisc \
#     rms

# RUN apt-get update -qq && apt-get -y --no-install-recommends install \
#     libjpeg-dev && \
#     install2.r --error \
#     --deps TRUE \
#     optparse

######## adding extra r-packages for days 2 and 5 scripts

# # use devtools to install markerGeneProfile
# RUN R -e 'remotes::install_github("oganm/markerGeneProfile", force = T, upgrade = "never")' \
#   && R -e 'remotes::install_github("oganm/ogbox", upgrade = "never")' \
#   && rm -rf /tmp/downloaded_packages/ /tmp/*.rds

# # use Bioconductor/BiocManager to install edgeR and DESeq2 GEOquery
# RUN  R -e 'BiocManager::install("edgeR", update = FALSE)' \
#   && R -e 'BiocManager::install("DESeq2", update = FALSE)' \
#   && R -e 'BiocManager::install("GEOquery", update = FALSE)'


# # installing SNF - it appears to be a monster..
# RUN apt-get update -qq && apt-get -y --no-install-recommends install \
#     wget curl git nano && \
#     install2.r --error \
#     SNFtool

# # adding day 2 ethics plyr depency - might go away
# RUN install2.r --error \
#     --deps TRUE \
#     plyr 

# RUN Rscript -e 'BiocManager::install("multtest")'
