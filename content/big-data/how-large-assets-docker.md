# How to Use FROM scratch Docker Images as an Asset Library for Large ML Assets (Models, Corpora) 

I'm starting to deal with large models and other ML-related assets, and need a solution for how to handle this inside the context of Docker development.

One might be tempted towards volumes. Unfortunately volumes are not portable between machines.

One _can_ simply bundle the assets directly into the image via as simple COPY. That works fine up to a point.

The problem is that one will likely want to be _efficient_, and so take as much advantage of Docker Image Layers as possible.

## Docker Images as Asset Library

[Docker multi-stage building](https://docs.docker.com/develop/develop-images/multistage-build/) to the rescue.

The trick is that one can use tagged images as a predefined ['stage'](https://docs.docker.com/develop/develop-images/multistage-build/#use-an-external-image-as-a-stage) of the build

To create an 'asset image' first create a Dockerfile for the image

```Dockerfile
FROM scratch
COPY <assets> /
```

Replace `<assets>` with the assets one wishes to preserve

Next build the image

```
build -t 'image_host/asset/foo:0.1' .
```

I'd suggest sticking with a naming convention that will make it obvious what it is being used for. I use `/asset` you do you.

Effectively the image tag becomes the [URI](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier) of the asset, which makes it easy both computationally and cognitively to deal with.

Importantly this tag is universal and can be pulled/pushed and referenced across machines using the existing Docker registry/repository infrastructure.

## Use Image Assets

```Dockerfile
COPY --from=image_host/asset/foo:0.1 / /assets/
```

For bonus points one can also use the [--link](https://docs.docker.com/engine/reference/builder/#copy---link) command to COPY if/when available.


## Summary

Using tagged images in combination with multi-stage builds, leads to quicker builds and deployments and more efficient use of disk space.

