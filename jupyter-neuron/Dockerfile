FROM continuumio/miniconda3

RUN conda install -y -q \
           "numpy" \
           "scipy" \
           "matplotlib" \
	   "pandas" \
           "pytest" \
           "seaborn" \
           "Cython" \
           "mpi4py" \
    && sync && conda clean --all && sync \
    && pip install --no-cache-dir  \
             "nilearn" \
             "tvb-library" \
	     "tvb-data" \
             "mne" \
	     "moviepy" \
	     "fooof" \
    && rm -rf ~/.cache/pip/*

# Neuron and lfpy installation
RUN conda config --add channels conda-forge
RUN conda install lfpy neuron=*=mpi*

## adding jupyter
RUN conda install jupyter

## adding compilation tools for lfpy
RUN conda install git make gxx_linux-64

## adding datalad layer
RUN conda install datalad

## adding dipy
RUN conda install dipy 
RUN pip install nilearn>=0.7

## installing wb_command
RUN apt-get update -qq && apt-get -y --no-install-recommends install libglu1 libgomp1 unzip\
  && wget https://www.humanconnectome.org/storage/app/media/workbench/workbench-linux64-v1.5.0.zip \
  && mkdir /content \
  && unzip workbench-linux64-v1.5.0.zip \
  && mv workbench /content/ \
  && rm workbench-linux64-v1.5.0.zip

ENV PATH        /content/workbench/bin_linux64/:$PATH

## trying to change workdir
WORKDIR /home/neuro

## this guy actually starts the jupyter notebook
CMD ["jupyter", "notebook", "--port=8888", "--no-browser", "--ip=0.0.0.0", "--allow-root"]
