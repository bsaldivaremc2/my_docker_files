FROM tensorflow/tensorflow:latest-gpu-jupyter
RUN apt-get install git

RUN pip install torch==1.12.1
RUN pip install torchvision==0.13.1
RUN pip install transformers==4.19.2
RUN pip install diffusers
RUN pip install invisible-watermark
#RUN pip install cuda-nvcc
#RUN pip install gcc
#RUN pip install gxx_linux-64=9.5.0

#xformers
RUN git clone https://github.com/facebookresearch/xformers.git
RUN cd xformers && git submodule update --init --recursive && pip install -r requirements.txt && pip install -e .

#mount file to share files
RUN mkdir -p /tf/mnt/

#stable_diffusion
RUN git clone https://github.com/Stability-AI/stablediffusion
RUN cd stablediffusion && pip install -r requirements.txt