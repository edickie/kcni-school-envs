# kcni-school-envs
A collection of docker environments for the KCNI Summer School

## The R, rstudio and plink env for day 1.

Building it manually (should only need to do this when editing as an instructor)

```sh
cd rstudio-plink
docker build -t rstudio-plink:v02 -t rstudio-plink:latest .  
```

Running the container (from local build)

```sh
docker run --rm \
 -p 127.0.0.1:8787:8787 \
 -e DISABLE_AUTH=true \
 -v <path/to/your/data>:/home/rstudio/data \
 rstudio-plink:latest
```

Note: on window's powershell the `\` character doesn't work - so the link above needs to be all on one line..

```sh
docker run --rm -p 127.0.0.1:8787:8787 -e DISABLE_AUTH=true -v C:\Users\erin_dickie\data\kcni-school-data\:/home/rstudio/kcni-school-data rstudio-plink:latest
```

Then open your browser and navigate to: http://localhost:8787/ and you should see your rstudio terminal!

## The Python-Octave Env for Physiological Modelling

Building the env (this may only need to be done by the instructor)

```sh
docker build -t neuron-py:v0.0 -t neuron-py:latest .  
```

Running the env

```sh
docker run --rm -p 8888:8888 -v C:\Users\erin_dickie\data\kcni-school-data\:/home/neuro/kcni-school-data neuron-py:latest
```

### new try - the neurodocker version is chunky and I can't get the neuron install inside - so now I'm gonna try miniconda3/jyputer as the base layer..

```sh
docker pull continuumio/miniconda3
docker run -i -t continuumio/miniconda3 /bin/bash
docker run -i -t -p 8888:8888 continuumio/miniconda3 /bin/bash -c "/opt/conda/bin/conda install jupyter -y --quiet && mkdir /opt/notebooks && /opt/conda/bin/jupyter notebook --notebook-dir=/opt/notebooks --ip='*' --port=8888 --no-browser"
```
