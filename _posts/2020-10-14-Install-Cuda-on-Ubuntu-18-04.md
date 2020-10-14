---
layout: post
title: Install Cuda on Ubuntu 18.04
subtitle: Nvidia
gh-repo: daattali/beautiful-jekyll
gh-badge: [settings]
tags: [cuda, nvidia, ubuntu]
comments: true

---
Hi các bạn, ở bài viết này mình sẽ huong dan cac ban cach cai dat cuda tren ubuntu 18.04
1. Start terminal and remove any NVIDIA traces you may have on your machine.

sudo rm /etc/apt/sources.list.d/cuda*
sudo apt remove --autoremove nvidia-cuda-toolkit
sudo apt remove --autoremove nvidia-*

2. Setup the correct CUDA PPA on your system

sudo apt update
sudo add-apt-repository ppa:graphics-drivers
sudo apt-key adv --fetch-keys  http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub
sudo bash -c 'echo "deb http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64 /" > /etc/apt/sources.list.d/cuda.list'
sudo bash -c 'echo "deb http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64 /" > /etc/apt/sources.list.d/cuda_learn.list'

3. Install CUDA 10.1 packages

sudo apt update
sudo apt install cuda-10-1
sudo apt install libcudnn7

or sudo apt install libcudnn10

4. As the last step one need to specify PATH to CUDA in ‘.profile’ file. Open the file by running:

sudo vi ~/.profile

And add the following lines at the end of the file:

# set PATH for cuda 10.1 installation
if [ -d "/usr/local/cuda-10.1/bin/" ]; then
    export PATH=/usr/local/cuda-10.1/bin${PATH:+:${PATH}}
    export LD_LIBRARY_PATH=/usr/local/cuda-10.1/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
fi
5. Restart and check the versions for the installation


[Source](https://medium.com/@exesse/cuda-10-1-installation-on-ubuntu-18-04-lts-d04f89287130)