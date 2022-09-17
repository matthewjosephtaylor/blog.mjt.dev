# How to run Stable Diffusion offline 2022

[Stable Diffusion](https://stability.ai/blog/stable-diffusion-public-release) is an open source Machine Learning (ML) model used for text to image generation.

It has a ['do no evil'](https://huggingface.co/spaces/CompVis/stable-diffusion-license) style license for those willing to be bound by it. IANAL you do you.

The major implication of this is that Huggingfaces has placed a small hurdle one must cross before downloading the model. To gain access to the model one must:
1. Have a hugging face account.
2. Click the 'I agree tot he license' button

The model card page is https://huggingface.co/CompVis/stable-diffusion-v1-4

To clone the repo with the model (requires account/click above)

```sh
$ git lfs install
$ git clone https://huggingface.co/CompVis/stable-diffusion-v1-4
```

Follow the code here