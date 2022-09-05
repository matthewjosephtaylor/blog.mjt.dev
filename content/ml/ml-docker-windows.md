# ML with Docker under Windows WSL2 2022

I've come to the point in my ML journey where I need to use my GPUs for ML/AI stuffs.


## An endless supply of nvidia docker containers and outdated documentation

There exists an unfortunate combination of 'cutting edge' combined with nvidia not having any competition.

Let's cut to the chase.

Here are the contianers that nvidia provides. You will use them and you will like it:

https://catalog.ngc.nvidia.com/containers

Here is some concise info on how the containers work:

https://github.com/NVIDIA/nvidia-docker/wiki

Here is the magic to get tensorflow to see GPUs in Docker
YMMV (Your Magic May Vary):

```Dockerfile
FROM nvcr.io/nvidia/tensorflow:22.08-tf2-py3

# Setup env for OS installs
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONFAULTHANDLER 1

# Specify a sane python environment
RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive TZ=Etc/UTC apt-get -y install tzdata
RUN apt-get install -y software-properties-common
RUN add-apt-repository ppa:deadsnakes/ppa
RUN apt-get install -y python3-pip
RUN apt-get install -y python3.9
RUN apt-get install -y python3.9-distutils

# Install pipenv and compilation dependencies
RUN pip install pipenv
RUN apt-get install -y --no-install-recommends gcc

# Attempt at a faster development loop by pre-installing python deps
COPY Pipfile* /app/
WORKDIR /app
RUN PIPENV_VENV_IN_PROJECT=1 pipenv install --deploy

# Application code
COPY app /app

# Magic nvidia variables
ENV NVIDIA_VISIBLE_DEVICES all
ENV NVIDIA_DRIVER_CAPABILITIES compute,video,utility

ENTRYPOINT ["pipenv", "run", "python3", "app.py"]
```

## WSL2 Docker GPU
Here is how to run docker under WSL2 with GPUs

```console
$ docker run --gpus all nvcr.io/nvidia/k8s/cuda-sample:nbody nbody -gpu -benchmark
```

## Loss Function
Simple python script to see how far away from victory you are:

```python
import tensorflow as tf
ds = tf.config.list_physical_devices()
print(ds)
```

When victory is achieved it will look something like:
```console
[PhysicalDevice(name='/physical_device:CPU:0', device_type='CPU'), PhysicalDevice(name='/physical_device:GPU:0', device_type='GPU'), PhysicalDevice(name='/physical_device:GPU:1', device_type='GPU')]
```
If you only see CPU devices, then you know further effort is required.