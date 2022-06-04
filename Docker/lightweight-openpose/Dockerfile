FROM nvidia/cuda:11.0-devel-ubuntu20.04

RUN apt-get update
RUN apt-get install -y python3 python3-pip

WORKDIR /mnt
ENV LIBRARY_PATH /usr/local/cuda/lib64/stubs