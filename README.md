# Singularity-image-for-Deep-Learning
## We assumed you have already been under speruser mode and Singularity has been installed properly.
- Grab the docker image of Ubuntu 16.04 LTS to the local directory
```singularity build --sandbox ub1604-python3-tensorflowr1.7-cuda8-gpu/ docker://ubuntu:xenial```

- Enter the OS of the image
```singularity shell --writable ub1604-python3-tensorflowr1.7-cuda8-gpu/```

- System update
```Singularity ub1604-python3-tensorflowr1.7-cuda8-gpu:~> apt-get update```

- Install system default python
```Singularity uub1604-python3-tensorflowr1.7-cuda8-gpu:~> apt-get install python3 python3-pip```

- Setup locality for pip
```Singularity ub1604-python3-tensorflowr1.7-cuda8-gpu:~> export LC_ALL=C```

- Install python3 module for tensorflow
```Singularity ub1604-python3-tensorflowr1.7-cuda8-gpu:~> apt-get install python3-numpy python3-dev python3-wheel python3-six```

- Download bazel 0.11.1 (bazel_0.11.1-linux-x86_64.deb) and install it
```
Singularity ub1604-python3-tensorflowr1.7-cuda8-gpu:~> apt-get install openjdk-8-jdk build-essential zip
Singularity ub1604-python3-tensorflowr1.7-cuda8-gpu:~> apt-get install bash-completion zlib1g-dev
Singularity ub1604-python3-tensorflowr1.7-cuda8-gpu:~> dpkg -i bazel_0.11.1-linux-x86_64.deb
```

- Install CUDA 8.0
```
Singularity ub1604-python3-tensorflowr1.7-cuda8-gpu:~> apt-get install git wget
Singularity ub1604-python3-tensorflowr1.7-cuda8-gpu:~> wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/cuda-repo-ubuntu1604_8.0.61-1_amd64.deb
Singularity ub1604-python3-tensorflowr1.7-cuda8-gpu:~> dpkg -i cuda-repo-ubuntu1604_8.0.61-1_amd64.deb
Singularity ub1604-python3-tensorflowr1.7-cuda8-gpu:~> apt-get update
Singularity ub1604-python3-tensorflowr1.7-cuda8-gpu:~> apt-get install cuda-8-0 cuda-toolkit-8-0
```

- Install CUDNN Download [Version 7.0.5 for CUDA8] (https://developer.nvidia.com/compute/machine-learning/cudnn/secure/v7.1.2/prod/8.0_20180316/cudnn-8.0-linux-x64-v7.1) as the example
```
Singularity ub1604-python3-tensorflowr1.7-cuda8-gpu:~> tar -xzvf cudnn-8.0-linux-x64-v7.1.solitairetheme8
Singularity ub1604-python3-tensorflowr1.7-cuda8-gpu:~> cp cuda/include/* /usr/local/cuda-8.0/include/
Singularity uub1604-python3-tensorflowr1.7-cuda8-gpu:~> cp cuda/lib64/* /usr/local/cuda-8.0/lib64/

```

- Install verbs (RDMA)
```
Singularity ub1604-python3-tensorflowr1.7-cuda8-gpu:~> apt-get install librdma* libibverbs1 ibacm ibutils infiniband-diags libibcm1 libibdm1v5 libibmad5 libibnetdisc-dev libibnetdisc5 libibumad3 libmlx5-1 libmthca1 libopensm5a libosmcomp3 libosmvendor4 libumad2sim0 opensm perftest srptools
```

- Install OpenMPI (optional)
```
Singularity ub1604-python3-tensorflowr1.7-cuda8-gpu:~> apt-get install openmpi-bin openmpi-common openmpi-doc libopenmpi-dev libopenmpi1.10
Singularity ub1604-python3-tensorflowr1.7-cuda8-gpu:~> export MPI_HOME=/usr/lib/openmpi
```

- Download tensorflow r1.7
```
Singularity ub1604-python3-tensorflowr1.7-cuda8-gpu:~> git clone https://github.com/tensorflow/tensorflow 
Singularity ub1604-python3-tensorflowr1.7-cuda8-gpu:~> cd tensorflow
Singularity ub1604-python3-tensorflowr1.7-cuda8-gpu:~> git checkout r1.7
```

- Install tensorflow r1.7
``` 
Singularity ub1604-python3-tensorflowr1.7-cuda8-gpu:~> cd tensorflow
Singularity ub1604-python3-tensorflowr1.7-cuda8-gpu:~> cd /usr/local/cuda-8.0/nvvm/libdevice && cp libdevice.compute_50.10.bc libdevice.10.bc
Singularity ub1604-python3-tensorflowr1.7-cuda8-gpu:~> ./configure \#answer the questions
Singularity ub1604-python3-tensorflowr1.7-cuda8-gpu:~> bazel build --config=opt --config=cuda --cxxopt="-D_GLIBCXX_USE_CXX11_ABI=0" //tensorflow/tools/pip_package:build_pip_package --config=monolithic
Singularity ub1604-python3-tensorflowr1.7-cuda8-gpu:~> bazel-bin/tensorflow/tools/pip_package/build_pip_package /tmp/tensorflow_pkg
Singularity ub1604-python3-tensorflowr1.7-cuda8-gpu:~> cd /tmp/tensorflow_pkg
Singularity ub1604-python3-tensorflowr1.7-cuda8-gpu:~> cp tensorflow-XXXXXX-linux_x86_64.whl ~/
Singularity ub1604-python3-tensorflowr1.7-cuda8-gpu:~> pip3 install tensorflow-XXXXXX-linux_x86_64.whl
```

- Make the Singularity image
```
singularity build ub1604-python3-tensorflowr1.7-cuda8-gpu.img ub1604-python3-tensorflowr1.7-cuda8-gpu/
```
