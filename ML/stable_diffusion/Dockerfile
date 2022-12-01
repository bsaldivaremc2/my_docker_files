FROM tensorflow/tensorflow:latest-gpu-jupyter
RUN apt-get install git
RUN mkdir mnt

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

#Version 1
RUN git clone https://github.com/CompVis/stable-diffusion
RUN cd stable-diffusion && conda env create -f environment.yaml
RUN conda install -n ldm pytorch torchvision -c pytorch
SHELL ["conda","run","-n","ldm","/bin/bash","-c"]
RUN echo "$CONDA_DEFAULT_ENV : starting stable diffusion v1." > tmp.txt
RUN pip install transformers==4.19.2 diffusers invisible-watermark
RUN cd stable-diffusion && pip install -e .
RUN echo "$CONDA_DEFAULT_ENV : finishing stable diffusion v1." >> tmp.txt

#Version 2
RUN git clone https://github.com/Stability-AI/stablediffusion
RUN echo "$CONDA_DEFAULT_ENV : starting stable diffusion v2." >> tmp.txt
RUN conda install -n ldm pytorch==1.12.1 torchvision==0.13.1 -c pytorch
#SHELL ["conda","run","-n","ldm","/bin/bash","-c"] #already activated
RUN pip install transformers==4.19.2 diffusers invisible-watermark
#RUN cd stablediffusion && pip install -r requirements.txt && pip install -e .
RUN cd stablediffusion && pip install -e .
RUN echo "$CONDA_DEFAULT_ENV : finishing stable diffusion v2." >> tmp.txt

#xformers requirements
#RUN export CUDA_HOME=/usr/local/cuda-11.4
#RUN conda install -c nvidia/label/cuda-11.4.0 cuda-nvcc
#RUN conda install -c conda-forge gcc
#RUN conda install -c conda-forge gxx_linux-64=9.5.0

#xformers
RUN git clone https://github.com/facebookresearch/xformers.git
RUN cd xformers && git submodule update --init --recursive && \
 pip install -r requirements.txt && \
 pip install -e .

#errors:
RUN echo "$CONDA_DEFAULT_ENV : starting error correction." >> tmp.txt
RUN apt-get update
RUN apt-get install ffmpeg libsm6 libxext6  -y
RUN apt-get install nano -y
RUN apt-get install apt-utils  -y
RUN pip install open_clip_torch # missing
RUN echo "$CONDA_DEFAULT_ENV : fixed for conda env after ImportError: libSM.so.6: cannot open shared object file: No such file or directory." >> tmp.txt
#Error in repo:
RUN cp -r stablediffusion/ldm/ stablediffusion/scripts/

RUN conda init bash
RUN source ~/.bashrc
