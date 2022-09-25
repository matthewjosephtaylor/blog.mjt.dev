# How to Conda (miniconda / anaconda) in Docker in 2022

In 2022 there are two incompatible paths to Python environment virtualization.

There is the [venv way](https://docs.python.org/3/tutorial/venv.html) and there is the [conda way](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html).

At the end of the day results are all that matter. No shade on conda. They are stepping forward and serving a real need.

The upshot of this is that effectively one has to choose, and unfortunately different libraries and projects are making different choices. Which just makes everyone's life that little bit harder.

Think of it like the Python 2 / 3 split. It is messy, complicated, and unfortunate.

# Docker for development and deployment

```Dockerfile

# Install Conda via shell script. It is is not in any main repo :(
RUN mkdir -p /opt/conda
RUN wget https://repo.anaconda.com/miniconda/Miniconda3-py38_4.12.0-Linux-x86_64.sh -O /opt/conda/miniconda.sh \
  && bash /opt/conda/miniconda.sh -b -p /opt/miniconda

# Install your environment.yaml deps into base env
# Uncomment once you are ready to start productionizing the image
# COPY environment.yaml /tmp
# RUN . /opt/miniconda/bin/activate && conda env update --name base --file /tmp/environment.yaml


# Install your softwares
# Uncomment once you have software to install
# RUN mkdir /app
# WORKDIR /app
# COPY * ./

# Run the software in conda base environment
CMD ["/opt/miniconda/bin/conda", "run", "--no-capture-output", "-n", "base", "python" "app.py"]

```

## Development

In VSCode open a new 'Remote (container)' using the above Dockerfile.

For conda virtual-environment shell access inside a terminal:
```shell
. /opt/miniconda/bin/activate
```
Recommend to select the [Conda 'base' python interpreter from inside VSCode](https://code.visualstudio.com/docs/python/environments#_conda-environments) once the devcontainer is running. Then any new terminal shells will be automagically activated. You will also need to install the [Python Plugin](https://marketplace.visualstudio.com/items?itemName=ms-python.python) inside the container (for 'reasons' remote development environments can't use the local plugin). Suggest ticking the gear icon and 'adding to devcontainer.json'

To install new python packages simply do

```shell
$ conda install <package>
```

This will install into the `base` environment which you have activated.


## Production
When one is ready to 'productionize' the image

```shell
$ conda env export > environment.yml
```

Then add/uncomment this snippet to the Dockerfile

```shell
COPY environment.yaml /tmp
RUN . /opt/miniconda/bin/activate && conda env update --name base --file /tmp/environment.yaml
```

## Summary

Using Conda inside Docker development container / production image is doable. 

The trick is to stick with the `base` environment. The container itself acts as the real 'virtual environment'.

