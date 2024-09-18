---
marp: true
theme: default
class: invert
size: 16:9
style: |
  img {background-color: transparent!important;}
  a:hover, a:active, a:focus {text-decoration: none;}
  header a {color: #148ec8 !important; font-size: 24px;}
  footer {color: #148ec8;}
header: '[Stable Diffusion 101](#1 " ")'
footer: 'Slides by [Hardip](https://hardippatel.com)'
---

# Hitchhiker's Guide to Text-To-Image Generation
#### [Hardip Patel](https://hardippatel.com)
#
#
[Presentation in blog format](https://hardippatel.com/memories/sd101)

* * *

## Intro

- Fulltime: Backend-Heavy Full-Stack developer
- Sparetime: Work on my [Accountability](https://hardippatel.com) site
- Hobbies:
    - Snooker (very recent)
    - Box Cricket
    - Try new hobbies
- Currently Reading
    - [Make by Pieter Levels](https://readmake.com)

* * *

## Why this topic? ...even though you're GenAI "noob"

- Provide beginner's perspective
- Wanted to help close the **barrier to entry** gap

* * *

## Inspiration ...for getting into it

- Want to create dynamically updating hero pic for my [Accountability](https://hardippatel.com) site
- [Pieter Levels](https://twitter.com/levelsio) (Check [Photo AI](https://photoai.com/))
- [Sayak Paul](https://huggingface.co/sayakpaul)
- [Overpowered](https://www.youtube.com/watch?v=IlIhykPDesE)
- [Abhishek Thakur](https://www.linkedin.com/in/abhi1thakur)

* * *

## Journey Overview

- Tried **Midjournery** on Discord very very early
- Tested **Automatic1111** after watching Overpowered
- Reached saturation with UI, so wanted to try with code
    - So hopped on to [Google Colab](https://colab.research.google.com)
- Tried **ComfyUI** for this talk and it is ***quite awesome*** to say the least

* * *

## What is Stable Diffusion?

- Text to Image model, combination of...
    - Language Model, to transform Text to Latent Representation
    - Generative Image Model, image conditioned on that Representation
- Based on Diffusion (Probablistic) Models
    - Class of Latent Variable Generative models

* * *

## UI Tools for No-Code

- Automatic1111
- ComfyUI
- Invoke AI
- DiffusionBee

* * *

## [Automatic1111](https://github.com/AUTOMATIC1111/stable-diffusion-webui)

[Installation Link](https://github.com/AUTOMATIC1111/stable-diffusion-webui?tab=readme-ov-file#installation-and-running)

- Widely used
- Good extension support
- Most compatible
- But unstable...

* * *

## ComfyUI

[Installation Link](https://github.com/comfyanonymous/ComfyUI?tab=readme-ov-file#installing)  
[Tutorial/Guide](https://comfyanonymous.github.io/ComfyUI_tutorial_vn/)

- Getting slack lately
- Intuitive UI
- Very stable

* * *

## Terminologies (1/5)

- PyTorch
    - deep learning framework based on Torch
- Base Model
    - Foundational model upon with specific model variants are made
    - For example, v1.5, v2, XL 0.9, XL 1.0
- Checkpoint (Model)
    - Pretrained Weights
    - Types of images model is trained on
    - For example, Juggernaut XL, Anything v3.0, epicRealism, etc...

* * *

## Terminologies (2/5)

- Guidance Scale (CFG)
    - Controls how much a process **follows a text prompt**
- **LoRA** ( **LO**w **R**ank **A**daptation Technology)
    - Add specific styles or characters while mantaining manageable file sizes
- **PEFT** (**P**arameter **E**fficient **F**ine-**T**uning)
    - Adapting Pre-trained Language Model(PLMs) to fine-tune extra parameters while keeping original parameters frozen.
    - Used to create LoRA

* * *

## Terminologies (3/5)

- Weights
    - Numerical values associated with the connections between neurons in neural network architecture
    - [Visualize](https://hackernoon.imgix.net/hn-images/1*_RLj3E4Lt8cZzlwtmcbqlA.png)
- Prompt
    - Text based instruction

* * *

## Terminologies (4/5)

- Text encoder
    - Transformer language model
    - Tokenizes text to be fed into U-Net
- U-Net
    - Takes encoded text (plain text processed into a format it can understand) and a noisy array of numbers as inputs
- VAE
    - Encodes and decodes images to and from a smaller latent space
- [Visualize](https://miro.medium.com/v2/resize:fit:1156/format:webp/1*ka4ci_UymoxuH4LAjiA6iw.png)

* * *

## Terminologies (5/5)

- Pipeline
    - Running diffusion models in inference by bundling all the necessary components.
    - Provides flexibility
- Seed
- Fine-Tuning
    - Train a wide dataset model on a narrow dataset model

* * *

## Code demo

- [Inference Code](https://gist.github.com/knightkill/a0f207c69068479686057a1293d2cfa0)
- [Model Fine-Tuning code](https://gist.github.com/knightkill/a0f207c69068479686057a1293d2cfa0)
    - Prepare Images for Training using [Birme](https://www.birme.net/)
    - [Don't use token which is already trained](https://github.com/2kpr/dreambooth-tokens/blob/main/all_single_tokens_to_4_characters.txt)
- [Inference code with trained model](https://gist.github.com/knightkill/d6a7db77ea6a6fcf2bad5eb14dcf0b7f)

* * *

# ComfyUI with trained model

* * *

## Further capabilities of Stable Diffusion

- Inpainting
    - Restore/Repair image
- Outpainting
    - Extend canvas of the image
- Image To Image
    - New image from input as image and text prompt
    - New image will follow the composition and color of input image
- Depth To Image
    - Take depth of the input image for composition of new image

* * *

# THAT'S ALL FOLKS!

* * *

## Credits

- [Towards Data Science](https://towardsdatascience.com)
- [Hugging Face](https://huggingface.co/docs)
- [Google Colab](https://colab.google)
- [BIRME](https://www.birme.net/)
- [Automatic1111](https://github.com/AUTOMATIC1111)
- [Comfy UI](https://github.com/comfyanonymous/ComfyUI)
