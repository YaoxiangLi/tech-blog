---
title: CUDA & cuDNN configuration for a Ubuntu 16.04 deep learning machine
categories: Deep Learning
abbrlink: 6656
date: 2017-09-21 11:03:30
tags:
    - Linux
    - CUDA
    - TensorFlow
---

## Install CUDA 8.0

```bash
sudo dpkg -i cuda-repo-ubuntu1604-8-0-local-ga2_8.0.61-1_amd64.deb

sudo apt-get update
sudo apt-get install cuda
```

## Update

```bash
sudo dpkg -i cuda-repo-ubuntu1604-8-0-local-cublas-performance-update_8.0.61-1_amd64.deb

sudo apt-get update
sudo apt-get upgrade
```

## Add libraries to .bashrc file,

```bash
echo 'export PATH=/usr/local/cuda/bin:$PATH' >> ~/.bashrc
echo 'export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH' >> ~/.bashrc
source ~/.bashrc
```

## After sourcing the bashrc file, the CUDA version can be verified using

```bash
nvcc -V
```

Next step is to install cuDNN. cuDNN can be downloaded from NVIDIA’s webpage https://developer.nvidia.com/cudnn.

Extract cuDNN and install.

```bash
cd ~/Downloads/
tar xvf cudnn*.tgz
cd cuda
sudo cp */*.h /usr/local/cuda/include/
sudo cp */libcudnn* /usr/local/cuda/lib64/
sudo chmod a+r /usr/local/cuda/lib64/libcudnn*
```

Once finished those above, install tensorflow in virtulenv and activate it.
