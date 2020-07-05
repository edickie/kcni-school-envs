FROM continuumio/miniconda3

## pre-reqs for NEURON
RUN apt-get update -qq \
      && apt-get install -y -q --no-install-recommends \
      apt-utils \
      bzip2 \
      ca-certificates \
      curl \
      locales \
      unzip \
     libx11-dev \
     git \
     bison \
     flex \
     automake \
     libtool \
     libxext-dev \
     libncurses-dev \
     xfonts-100dpi \
     libopenmpi-dev \
     tar \
     make \
     zlib1g-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

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
    && rm -rf ~/.cache/pip/*

# Neuron and lfp installatin
RUN conda config --add channels conda-forge
RUN conda install lfpy neuron=*=mpi*

## adding jupyter
RUN conda install jupyter

## this guys actually starts the jupyter notebook
CMD ["jupyter", "notebook", "--port=8888", "--no-browser", "--ip=0.0.0.0", "--allow-root"]
