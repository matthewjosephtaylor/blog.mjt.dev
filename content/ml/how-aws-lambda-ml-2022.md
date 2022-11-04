# How To Machine Learning Inference Using AWS Lambda in 2022

It is one thing to create a Jupyter notebook to train and test models. It is quite another to deploy those models into production.

Code is messy. It combines elements from across a wide sea of libraries to craft a particular solution. There is no 'one size fits all'.

Machine learning pipelines aren't just the model weights. There can be significant pre and post processing that happens to get the input data into the correct form, and craft output as an easy to work with result.

The technique I'm about to describe is not the best fit for all situations. In fact, it is a hack for this moment in 2022 when Machine Learning is still geared more towards the needs of a data scientist vs a software engineer.

YOU HAVE BEEN WARNED!

## Development Environment

- Use [VSCode](https://code.visualstudio.com/)
- Use [Docker](https://www.docker.com/)
- Use [AWS SAM CLI](https://aws.amazon.com/serverless/sam/)

Use SAM CLI to create a project folder using the AWS/MachineLearning/Python3.9 template.

Note we are creating an _image-based_ AWS Lambda that will contain all the model weights, etc.

Inside of VSCode use a [Dev Container](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) to perform all coding tasks.

I suggest using [Pipfile](https://github.com/pypa/pipfile) as the least-bad solution to Python library dependencies in 2022 that works well with VSCode. Note that the use of some libraries will mandate other solutions such as [Anaconda](https://www.anaconda.com/products/distribution).

SAM CLI `template.yaml` interesting bits:
  - Globals/Function/Timeout
  - Globals/Function/MemorySize
  - Resources/InferenceFunction/Properties/Events/Inference/Properties/Metadata/DockerTag

## Development Loop

I recommend creating a simple '__main__' function that calls your main entrypoint function vs using `sam local invoke` for most development. This will allow you to stay comfortably inside the Dev Container.

Be cognizant of how the `lambda_handler` _event_ data is handled. If your payload is a JSON string it will magically _parse_ the string into a JSON object for you inside your Python code. IMHO poor/confusing design but such is life.

## Large Assets

Almost certainly one will be using [NLTK](https://www.nltk.org/) and/or [Huggingface](https://huggingface.co/) and/or other similar libraries/frameworks.

It is IMPORTANT to note that these libraries are 100% geared towards making the life of a data-scientist easy. Unfortunately that means making the life of a software engineer difficult.

The main problem with these libraries is that there is no consistent standard for dealing with the large assets such as model-weights, copora, etc.

In fact each library does their best to _hide_ the existence of these large data objects by automagic on-demand downloading only as needed. The most reliable way I've discovered to root out the magic is to watch the $HOME folder like a hawk as code is being run. Then work through each library's documentation on how to 'defeat' the magic and pre-load the data.

Here is a snippet of my current Dockerfile template:

```Dockerfile
# prevent __pycache__
ENV PYTHONDONTWRITEBYTECODE="1"

# Single home for all caches that can be saved in an asset layer
ENV XDG_CACHE_HOME="/cache"
ENV HF_HOME="/cache/huggingface"
ENV HF_DATASETS_CACHE="/cache/huggingface/datasets"
ENV TRANSFORMERS_CACHE="/cache/huggingface/transformers"
ENV HUGGINGFACE_HUB_CACHE="/cache/huggingface/hub"
ENV TORCH_HOME="/cache/torch"
RUN mkdir -p /cache/nltk_data
ENV NLTK_DATA="/cache/nltk_data"
RUN mkdir -p /cache/gensim-data
ENV GENSIM_DATA_DIR="/cache/gensim-data"
```
Your pain will vary but perhaps this gives a good base to start from / something to google.

Note that the comment says something about an 'asset layer'. Here is where I add my own bit of magic to the mix.

Through a bit of trial and error I've discovered a neat pattern for efficiently dealing with large asset data in the context of Docker images.

I describe the [Docker Image Asset Library pattern in this article](https://mjtdev.medium.com/how-to-use-from-scratch-docker-images-as-an-asset-library-for-large-ml-assets-such-as-models-a2519c213e7c). I don't claim to be the first to have discovered this pattern, but I don't see it widely talked about.

Create a tarball of all the relevant files (model-weights, corpora, etc..) in the $HOME folder, and then create an 'Asset Image' that can be published to your AWS docker repository using that tarball. 

Pushing the Asset Image to a seperate repository isn't _strictly needed_ but is handy as it gives the asset a good _name_ that can be referenced later if someone else wants to _build_ the project from source.

Use the Asset Image inside the main Lambda image you will be publishing to AWS.

Example of how to use an Asset Image:
```Dockerfile
COPY --from=<AWS ECR REPO>/foo-model-weights:latest / /
```

## AWS Lambda Usage

Don't even think of using anything other than 'invoke' via the [AWS SDK](https://aws.amazon.com/developer/tools/) for interacting with the Lambda. Using the HTTP gateway API is just asking for pain and timeouts.


## Summary

Serving custom 'serverless' ML pipelines in 2022 is a pain. I have hopes this will improve a bit with standards such as [ONNX](https://onnx.ai/) making at least the model serving more standardized.

In the meantime, with a bit of extra thought and care one can use typical ML-focused Python libraries / code to serve ML pipelines in a production cloud-based environment. 

When you put all the pieces together it works pretty well, but there is much 'assembly required'. Good Luck! :)
