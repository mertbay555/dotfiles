## CUDA installation guide:
http://docs.nvidia.com/cuda/cuda-installation-guide-linux/#axzz4VZnqTJ2A
```
$ lspci | grep -i nvidia
$ uname -m && cat /etc/*release
$ gcc --version
```

## Install LINUX headers
```
$ sudo apt install linux-headers-$(uname -r)
```

## Download and install CUDA 8.0
For GTX 1080 Ti, select No to install NVidia driver 376.
```
$ wget https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_375.26_linux-run
$ sudo sh cuda_8.0.61_375.26_linux-run
```

For GTX 1080 Ti, you need to install NVidia driver 381.09 manually
```
$ sudo add-apt-repository ppa:graphics-drivers/ppa
$ sudo apt update
$ sudo apt -y install nvidia-381
```

If the installation fails, remove X lock in /tmp.

## Disable Nouveau if a command below displays anything:
```
$ lsmod | grep nouveau
```

Create a file at /etc/modprobe.d/blacklist-nouveau.conf with the following # contents:
```
blacklist nouveau
options nouveau modeset=0
```
Then regenerate the kernel initramfs:
```
$ sudo update-initramfs -u
```

## Install cuDNN 5.1
Download cuDNN from https://developer.nvidia.com/cudnn
```
$ sudo cp include/cudnn.h /usr/local/cuda/include
$ sudo cp -P lib64/libcudnn* /usr/local/cuda/lib64/
$ sudo chmod a+r /usr/local/cuda/include/cudnn.h
$ sudo chmod a+r /usr/local/cuda/lib64/libcudnn*
```

## Install NVIDIA CUDA Profile Tools
```
$ sudo apt install libcupti-dev
```

## Install TensorFlow
```
$ sudo pip install -U tensorflow-gpu
```

## Install Keras
```
$ sudo pip install keras
```

## To uninstall all nvidia drivers
```
sudo apt-get remove --purge nvidia-*
sudo apt-get install ubuntu-desktop
```
