---
title: 'Upgrade to TensorFlow 1.6, CUDA 9.0 and cuDNN v7.1.1'
categories: Deep Learning
abbrlink: 33117
date: 2018-03-12 18:10:52
tags:
    - TensorFlow
    - CUDA
    - cuDNN
---
Since from the release of TensorFlow r1.6 it starts to support CUDA9.0, upgrade to CUDA from 8.0 to 9.0 is a must.

Firstly, download all the installation files from NVIDIA.

## Install CUDA 9.0

```bash
sudo dpkg -i cuda-repo-ubuntu1604-9-0-local_9.0.176-1_amd64.deb

sudo apt-get update
sudo apt-get install cuda
```

Use the autoremove to remove CUDA 8.0

```bash
sudo apt-get autoremove
```

## Update

```bash
sudo dpkg -i cuda-repo-ubuntu1604-9-0-local-cublas-performance-update_1.0-1_amd64.deb

sudo apt-get update
sudo apt-get upgrade
```

```bash
sudo dpkg -i cuda-repo-ubuntu1604-9-0-local-cublas-performance-update-2_1.0-1_amd64.deb

sudo apt-get update
sudo apt-get upgrade
```

## Modify the .bashrc file

```bash
export PATH=/usr/local/cuda-9.0/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda-9.0/lib64:$LD_LIBRARY_PATH
```

Then source it.

```bash
source ~/.bashrc
```

## After sourcing the bashrc file, the CUDA version can be verified using

```bash
nvcc --version
```

## Restart system for the graphic dirver R384 to take effect

Then check it:

```bash
nvidia-smi

+-----------------------------------------------------------------------------+
| NVIDIA-SMI 384.111                Driver Version: 384.111                   |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  GeForce GTX 970M    Off  | 00000000:01:00.0 Off |                  N/A |
| N/A   53C    P0    26W /  N/A |    564MiB /  6078MiB |     12%      Default |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID   Type   Process name                             Usage      |
|=============================================================================|
|    0      1192      G   /usr/lib/xorg/Xorg                           263MiB |
|    0      2020      G   compiz                                       133MiB |
|    0      3776      G   ...-token=794ED49FD68C1309792D9D8F291D5B68   165MiB |
+-----------------------------------------Haven't you observed the same problem?

------------------------------------+
```

Next step is to install cuDNN. cuDNN can be downloaded from NVIDIA’s webpage:[cuDNN page](https://developer.nvidia.com/cudnn).

Extract cuDNN and install.

```bash
tar xvf cudnn-9.0-linux-x64-v7.1.tgz
sudo cp cuda/include/cudnn.h /usr/local/cuda/include
sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64
sudo chmod a+r /usr/local/cuda/include/cudnn.h /usr/local/cuda/lib64/libcudnn*
```

Then install tensorflow r1.6 as the TensorFlow official website instructed in venv.

After installation, try the TensorFlow validation, it will work. However, When dealing with Keras predict model, it will raise such errors:

## Downgrade to cuDNN v7.0.5

```bash
E tensorflow/stream_executor/cuda/cuda_dnn.cc:378] Loaded runtime CuDNN library: 7101 (compatibility version 7100) but source was compiled with 7004 (compatibility version 7000).  If using a binary install, upgrade your CuDNN library to match.  If building from sources, make sure the library loaded at runtime matches a compatible version specified during compile configuration.
```

Obveriously, it is a problem about cuDNN version compatibility. Solving this problem by downgrade the cuDNN to cuDNN v7.0.5 (Dec 5, 2017), for CUDA 9.0.

```bash
tar xvf cudnn-9.0-linux-x64-v7.tgz
sudo cp cuda/include/cudnn.h /usr/local/cuda-9.0/include
sudo cp cuda/lib64/libcudnn* /usr/local/cuda-9.0/lib64
sudo chmod a+r /usr/local/cuda-9.0/include/cudnn.h /usr/local/cuda-9.0/lib64/libcudnn*
```

Enjoy!