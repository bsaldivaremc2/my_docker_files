FROM tensorflow/tensorflow:latest-gpu-jupyter
RUN apt-get install git

#Conda instructions from https://fabiorosado.dev/blog/install-conda-in-docker/
# Install base utilities
RUN apt-get update && \
    apt-get install -y build-essential  && \
    apt-get install -y wget && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install miniconda
ENV CONDA_DIR /opt/conda
RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh && \
     /bin/bash ~/miniconda.sh -b -p /opt/conda

# Put conda in path so we can use conda activate
ENV PATH=$CONDA_DIR/bin:$PATH

RUN git clone https://github.com/CompVis/stable-diffusion
RUN cd stable-diffusion && conda env create -f environment.yaml
RUN conda install -n ldm pytorch==1.12.1 torchvision==0.13.1 -c pytorch
#RUN conda init bash
#RUN source ~/.bashrc
#RUN conda activate ldm
#SHELL ["conda","activate","ldm"]
SHELL ["conda","run","-n","ldm","/bin/bash","-c"]
RUN pip install transformers==4.19.2 diffusers invisible-watermark
RUN cd stable-diffusion pip install -e .
