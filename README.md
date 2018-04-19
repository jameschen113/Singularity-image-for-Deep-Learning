# Singularity-image-for-Deep-Learning

## Grab the docker image of Ubuntu 16.04 LTS to the local directory
```singularity build --sandbox ub1604-python3-tensorflowr1.7-cuda8-gpu/ docker://ubuntu:xenial```

## Enter the OS of the image
```singularity shell --writable ub1604-python3-tensorflowr1.7-cuda8-gpu/```

## System update
```apt-get update```

## Install system default python
```apt-get install python3 python3-pip```

## Setup locality for pip
```export LC_ALL=C```

## Install python3 module for tensorflow
```apt-get install python3-numpy python3-dev python3-wheel python3-six```

## Download bazel 0.11.1 (bazel_0.11.1-linux-x86_64.deb) and install it
```apt-get install openjdk-8-jdk build-essential zip```
```apt-get install bash-completion zlib1g-dev```
```dpkg -i bazel_0.11.1-linux-x86_64.deb```

## Install CUDA 8.0
```apt-get install git wget```
```wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/cuda-repo-ubuntu1604_8.0.61-1_amd64.deb```
```dpkg -i cuda-repo-ubuntu1604_8.0.61-1_amd64.deb```
```apt-get update```
```apt-get install cuda-8-0 cuda-toolkit-8-0```

## Install CUDNN Download [Version 7.0.5 for CUDA8] (https://developer.nvidia.com/compute/machine-learning/cudnn/secure/v7.1.2/prod/8.0_20180316/cudnn-8.0-linux-x64-v7.1) as the example
```
tar -xzvf cudnn-8.0-linux-x64-v7.1.solitairetheme8
cp cuda/include/* /usr/local/cuda-8.0/include/
cp cuda/lib64/* /usr/local/cuda-8.0/lib64/
```

## Install verbs (RDMA)
```
apt-get install librdma* libibverbs1 ibacm ibutils infiniband-diags libibcm1 libibdm1v5 libibmad5 libibnetdisc-dev libibnetdisc5 libibumad3 libmlx5-1 libmthca1 libopensm5a libosmcomp3 libosmvendor4 libumad2sim0 opensm perftest srptools
```

## Install OpenMPI (optional)
```
apt-get install openmpi-bin openmpi-common openmpi-doc libopenmpi-dev libopenmpi1.10
export MPI_HOME=/usr/lib/openmpi
```

