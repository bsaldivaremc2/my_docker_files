FROM stable_diffusion_conda_req
RUN git clone https://github.com/CompVis/stable-diffusion
RUN conda activate ldm
RUN pip install transformers==4.19.2 diffusers invisible-watermark
RUN pip install -e .
#
RUN git clone https://github.com/facebookresearch/xformers.git
RUN cd xformers && \
 git submodule update --init --recursive && \
 pip install -r requirements.txt && \
 pip install -e .
