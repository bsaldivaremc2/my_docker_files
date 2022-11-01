# This is a docker image for an automl package called autogluon   


## Contents:  
- Autogluon 0.5.2, requirements gotten from https://auto.gluon.ai/stable/index.html  
- It has a gpu compatible docker image as base which also has a jupyter notebook.  
  
## Usage:  
- Get the image:  
```console
sudo docker pull bsaldivar/gpu_autogluon:0.5.2  
```
- Run the image and get a jupyter notebook server running 
```console
sudo  docker run -it --rm --gpus all -p 8888:8888 bsaldivar/gpu_autogluon:0.5.2
```
- Run the image and get a jupyter notebook server running but in a port different than 8888, e.g. 9999
```console
sudo  docker run -it --rm --gpus all -p 9999:8888 bsaldivar/gpu_autogluon:0.5.2
```
- Run the image with a console, so you could run on terminal
```console
sudo  docker run -it --rm --gpus all bsaldivar/gpu_autogluon:0.5.2 /bin/bash
```
The image has as the working directory **/tf/**, I added **/tf/mnt/** for more explicit interaction for sharing files with the container. To mount your **/home/yourusername/data/** directory to the **/tf/mnt/** directory do:  
```console
sudo  docker run -it -v /home/yourusername/data/:/tf/mnt/ --rm --gpus all -p 9999:8888 bsaldivar/gpu_autogluon:0.5.2
```
Therefore, if you create your juyter notebooks or results in the /tf/mnt/ directory, inside the container, they will appear on your /home/yourusername/data/ directory.

## Disclaimer:  
I am not the author of the autogluon paper nor original repository. I just wanted to provide an easy and reproducible access to their methods.