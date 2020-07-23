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

## this guy actually starts the jupyter notebook
CMD ["jupyter", "notebook", "--port=8888", "--no-browser", "--ip=0.0.0.0", "--allow-root"]
