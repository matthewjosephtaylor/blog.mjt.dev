# A Practical Guide to Serve Huggingface ML Models in AWS in Sept 2022

I'm a software developer with an interest in ML/AI. My perspective is more from a real-world application development side, not research or academia.

You have been warned. :)

This solution assumes a spiky batch-oriented usage model where the model is happy enough being served from a CPU.

This is very much a problem that has no 'one size fits all' solution. The provider landscape is changing at a rapid pace. AWS likely won't be the best solution for all. I would also take a peek at [SageMaker](https://aws.amazon.com/sagemaker) if one is thinking of AWS/ML and has a large enough usecase. 

At the end of the day it is about the balance of cost/performance, which also includes development/maintenance (developer/ops time) costs.

## Steps

1. Create an [AWS Lambda Function](https://aws.amazon.com/lambda/) using [AWS SAM CLI](https://github.com/aws/aws-sam-cli)
2. Write a bit of Python that serves the model
3. Deploy your model using `sam deploy --guided`
4. Fight the AWS permissions battles
5. Call the Lambda using [AWS SDK invoke](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/Lambda.html#invoke-property) from language of choice

Easy right? The Devil is in the details.

## Real World Problems

The model is not the begining nor the end of the story. It is the middle.

A quarter of the battle is wrestling data _into_ the model (preprocessing).

Half the battle is infering from the model (inference / prediction).

The last quarter of the battle is wrestling data from the model to the outside world (postprocessing)

The data science discipline comes more from statistics, not software. That is important to remember.

The current tools of data science are tuned more for research than for production use. In 2022 bridging the gap between research and production for any non-trivial application is the challenge.

## Heavy Dependencies

In addition to the model weights of the 'main model' it is quite likely that a variety of other 3rd party models and data are going to be used.

Dependency management means more than simple code dependencies for ML.

We are still a bit early in the age of data science used in production so the dependency problem is quite messy.

I note that there are not generally adopted 'clean' data resolution strategies (yet) for ML. 

The quick-n-dirty method most ML project have adopted: Dump data into the users home folder under their own sub-directory, managed in their own unique and special ways. Let a thousand caches bloom.

## De-magic-ing the Magic

[Huggingface](https://huggingface.co/) is a wonderful resource for exploring and working with models.

[NTLK](https://www.nltk.org/) is a wonderful library for performing a variety of natural language tasks. 

[gensim](https://github.com/RaRe-Technologies/gensim) is a wonderful library for topic modeling.

The list goes on and on and on. If you have an ML-related problem domain, there is likely at least one Python library/resource that has you covered (probably several).

The problem all these wonderful free resources is that they are all written and designed from the POV of research and data exploration. They are not designed with much thought for deployment in a production environment.

The practical upshot is that one has to _discover_ through trial and error how to deploy the multi-Mb (perhaps multi-Gb) data these resources provide inside a production environment.

I find that the simplest most naive approach is generally the most robust.

My current recommendation is simply to:

1. Run the project code inside a Docker container
2. Inspect the `/root` or $HOME folder to see what got dropped inside
3. Run `tar -cvf filename <cache-folder-name>`
4. Copy the tarball to somewhere outside the container
5. Add to Dockerfile `ADD cache-file.tar /cache` as needed
6. Set `ENV <resource-data-dir>="/cache/<resource-data>" as needed

Examples of cache folders found in $HOME:
- `.cache/huggingface` 
- `ntlk_data`
- `gensim-data`


Dockerfile Example Snippet
```Dockerfile
ENV HUGGINGFACE_HUB_CACHE="/cache/.cache/huggingface/hub"
ENV NLTK_DATA="/cache/nltk_data"
ENV GENSIM_DATA_DIR="/cache/gensim-data"
```

NOTE: $HOME in the Lambda running inside AWS will NOT be /root, and will not be writable.

Note that this is a messy, cumbersome, failure-prone, adhoc process. Such is life today. Good luck adventurer!

## How to Get Inferences

DO NOT USE THE AWS API GATEWAY!

There is a hard limit of 29 seconds on that gateway, and it is in addition flakey with a large warmup time in my experience. 

By far the better method is to use 'invoke' via the 
[AWS SDK](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/Lambda.html#invoke-property).

It is probably better these days to imagine AWS not having direct https support for its vast array of APIs and services. It is too large a beast, and needs a dedicated interpreter/ambassador to negotiate on one's behalf.

## Summary and Prediction

AWS Lambda for serving ML models can work well for small/medium sized ML tasks that need to scale from zero with a spiky workload.

Data science != ML Ops or application development.

We are in the _very_ early days of ML being used in production environments, it can only get better from here.

Predictions:
- A centralized/standardized winner will emerge who can solve the current mess of the 'every project has its own solution' data-dependency problem. A sort of npm or maven for organized large data/models. My bet would be huggingface.
- A language-neutral ML assembly language will emerge that will allow for incorporation of the pre/post pipeline processing in addition to pure ML processing.
- AWS Lambda will soonish have GPU/TPU capabilities.