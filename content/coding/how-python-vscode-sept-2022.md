# How to VSCode, Docker and Python in Sept 2022

I am an experienced coder but I am not a [Python](https://www.python.org) expert.

Recently I've been getting more and more into ML, and so have been interacting more with python.

I'll be honest and admit that I've avoided Python as it frustrates me.

But the only tool that isn't complained about, is the tool that is never used. Everything has its flaws. :)

# How I Deal with Python and Keep My Sanity

Like a lot of 'early' languages, Python has a dependency management and versioning problem. This IMHO is the _heart_ of most issues in Python, and has plagued the language for as long as I've been aware of it.

I therefore have adopted the following tools and patterns which so far works well to isolate environments:
- [Pipenv](https://pipenv.pypa.io/en/latest/)
- [Vscode](https://code.visualstudio.com/)
- [Docker](https://www.docker.com/)
- [Remote Containers](https://code.visualstudio.com/docs/remote/containers)


## Pipenv
I use the following environment variables for development directly on my loptop hardware:

```sh
# pipenv create .venv in local project dir similar to node_modules
export PIPENV_VENV_IN_PROJECT=1
export PIPENV_VERBOSITY=-1
```

The above will create a `.venv` directory at the root of the project. This allows VSCode to automagically detect the virtual-environment for things like code completion, terminal CLI exectution, etc...

The Pipfile itself appears to be 'ok' for capturing dependencies. I'm sure there are frustrations around transitive dependency handling, etc, but it works well enough for what it is. Note that the choice of this tool is the the heart of the 'battle' for Python, and so this recommendation may well change in the future and is the one I'm least happy with.

## VSCode 'Remote' Development

Likely one will need to deploy Python code in a linux-like environment.

I've personally found it easier over the years to develop in an environment as close to the 'production environment' as possible.

Containerized development is a 'must have' for 'serious Python' IMHO. The main use case for this language (AI/ML) involves using it as a 'glue language'. Most of the heavy lifting is going to be done in 'native library' code. In 2022 'native' === 'Some specified variant of Linux'.

Setup for containerized development can be found here: https://code.visualstudio.com/docs/remote/containers-tutorial

NOTE: You will need to (re)install the Python VSCode plugin as a 'remote development plugin' 
https://marketplace.visualstudio.com/items?itemName=ms-python.python after you've created your container.

After initial setup of your 'remote container' (which is a bit of a misnomer IMHO):

To `.devcontainer/devcontainer.json` add:

```json
	"remoteEnv": {
		"PIPENV_VENV_IN_PROJECT":"1",
		"PIPENV_VERBOSITY":"-1"
	}
```

I also recommend adding to the same file:

```json
	"postCreateCommand": "touch /root/.bashrc"
```
As most containers will not be setup for root interactive shell

Recommend using the same Dockerfile one will is in production for development (or at least as close as possible) and using the 'Remote Container from Dockerfile' option when setting up the VSCode 'Remote Container'.

## Example Dockerfile for playing around with Python

```Dockerfile
FROM ubuntu:22.04
RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive TZ=Etc/UTC apt-get -y install tzdata
RUN apt-get install -y software-properties-common
RUN add-apt-repository -y  ppa:deadsnakes/ppa
RUN apt-get install -y python3.9
RUN apt-get install -y python3.9-distutils
RUN apt-get install -y pip
# Fix annoying deprecated warning Bug https://askubuntu.com/a/1407138
RUN pip install --upgrade --user setuptools==58.3.0
RUN pip install pipenv
```

## Summary and Prediction

Python as used for ML is a ['glue language'](https://en.wikipedia.org/wiki/Scripting_language#Glue_languages) with an unfortunate story for dependency management and language compatability.

Fortunately there are tools/techniques such as Docker Containers and ['python virtual environments'](https://docs.python.org/3/library/venv.html) one can adopt to make the most of a messy situation.

## Predictions
- Pipenv/Pipfile will likely be replaced, but .venv or its equivalent/ancestor is here to stay.
- 'Remote' container development will increasingly become a recognized standard development technique.
- As ML fever gradually matures into a distinct discipline, the need for Python will be replaced as the community converges to a recognized 'assembly language' that can be run on any corresponding 'virtual machine' (probably based on Tensorflow or ONNX once they agree to something like a ['POSIX'](https://en.wikipedia.org/wiki/POSIX) I/O layer/standard). Much as [WASM](https://webassembly.org)/[WASI](https://wasi.dev) removes the need to use the Javascript language for 'web development'.
- Python will continue for the immediate future as a much maligned necessity, and will perform a similar function as 'Bash' does today: ugly, universal and 'good enough'.
