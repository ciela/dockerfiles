FROM nvidia/cuda
MAINTAINER ciela <zektbach@gmail.com>

RUN apt update -y && apt upgrade -y
RUN apt install -y python3-pip
RUN pip3 install --upgrade pip
RUN pip3 install http://download.pytorch.org/whl/cu90/torch-0.3.0.post4-cp35-cp35m-linux_x86_64.whl 
RUN pip3 install torchvision
