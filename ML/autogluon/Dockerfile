FROM tensorflow/tensorflow:latest-gpu-jupyter
RUN pip3 install -U pip
RUN pip3 install -U setuptools wheel
# Install the proper version of PyTorch following https://pytorch.org/get-started/locally/
RUN pip3 install torch==1.12.0+cu113 torchvision==0.13.0+cu113 torchtext==0.13.0 --extra-index-url https://download.pytorch.org/whl/cu113
RUN pip3 install autogluon
RUN pip3 install bokeh==2.0.1
#try these:
#RUN apt install cmake -y
#RUN pip uninstall lightgbm -y
#RUN pip install lightgbm --install-option=--gpu

#mount file to share files
RUN mkdir -p /tf/mnt/
#
