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
             "LFPy" \
    && rm -rf ~/.cache/pip/*

RUN curl -fsSL --retry 5 -o /tmp/nrn-7.7.deb https://neuron.yale.edu/ftp/neuron/versions/v7.7/nrn-7.7.x86_64-linux.deb \
    && dpkg -i /tmp/nrn-7.7.deb \
    && rm /tmp/nrn-7.7.deb \
    && echo "export PATH=$PATH:/usr/local/nrn/x86_64/bin" >> .bashrc

RUN pip install neuron

## adding jupyter
RUN conda install jupyter

## this guys actually starts the jupyter notebook
CMD ["jupyter", "notebook", "--port=8888", "--no-browser", "--ip=0.0.0.0", "--allow-root"]
