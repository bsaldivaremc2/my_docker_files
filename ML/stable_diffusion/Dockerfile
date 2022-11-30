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

#cv2 requirements
RUN apt-get update
RUN apt-get install ffmpeg libsm6 libxext6  -y

#stable_diffusion
RUN git clone https://github.com/Stability-AI/stablediffusion
RUN cd stablediffusion && pip install -r requirements.txt

#download weights
RUN apt-get install wget
RUN mkdir weights
RUN cd weights && wget https://huggingface.co/stabilityai/stable-diffusion-2/blob/main/768-v-ema.ckpt
