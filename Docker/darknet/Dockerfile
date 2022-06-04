FROM nvcr.io/nvidia/cuda:10.2-cudnn7-devel-ubuntu18.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt update && apt install -y --no-install-recommends \
    build-essential cmake unzip pkg-config \
    libjpeg-dev libpng-dev libtiff-dev \
    libavcodec-dev libavformat-dev libswscale-dev \
    libv4l-dev libxvidcore-dev libx264-dev \
    libgtk-3-dev libatlas-base-dev gfortran \
    ffmpeg python3-dev nano curl git \
    && rm -rf /var/lib/apt/lists/*
RUN curl https://bootstrap.pypa.io/pip/3.6/get-pip.py -o get-pip.py
RUN python3 get-pip.py && rm get-pip.py
RUN pip3 install --no-cache-dir numpy

WORKDIR /opt
ENV CV_VER=3.4.0
RUN curl -L https://github.com/opencv/opencv/archive/${CV_VER}.zip -o opencv-${CV_VER}.zip \
    && curl -L https://github.com/opencv/opencv_contrib/archive/${CV_VER}.zip -o opencv_contrib-${CV_VER}.zip

RUN unzip opencv-${CV_VER}.zip \
    && unzip opencv_contrib-${CV_VER}.zip \
    && rm opencv-${CV_VER}.zip opencv_contrib-${CV_VER}.zip

WORKDIR /opt/opencv-${CV_VER}
RUN mkdir build && cd build \
    && cmake -D WITH_CUDA=ON \
    -D WITH_CUDNN=ON \
    -D OPENCV_DNN_CUDA=ON \
    -D ENABLE_FAST_MATH=1 \
    -D CUDA_ARCH_BIN=7.5 \
    -D WITH_CUBLAS=1 \
    -D BUILD_opencv_python3=ON \
    -D BUILD_opencv_python2=OFF \
    -D BUILD_TESTS=OFF \
    -D BUILD_PERF_TESTS=OFF \
    -D BUILD_EXAMPLES=OFF \
    -D CMAKE_BUILD_TYPE=RELEASE \
    -D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib-${CV_VER}/modules \
    -D CMAKE_INSTALL_PREFIX=/usr/local .. \
    && make -j"&(nproc)" \
    && make install -j"&(nproc)" \
    && make clean

RUN echo $(pkg-config --modversion opencv)