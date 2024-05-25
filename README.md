# Text-to-Image Generation with Stable Diffusion

This project demonstrates how to generate images from textual descriptions using a pretrained model from the Stable Diffusion framework. The script leverages Google Colab for GPU acceleration to enhance computation efficiency.

## Table of Contents
- [Introduction](#introduction)
- [Installation](#installation)
- [Usage](#usage)
- [Key Components](#key-components)
- [Practical Applications](#practical-applications)
- [License](#license)

## Introduction

This project utilizes a pretrained text-to-image generation model from StabilityAI to create images based on textual prompts. The model, part of the Stable Diffusion framework, generates high-quality images by interpreting the given text.

## Installation

To set up the environment and install the necessary dependencies, use the following commands in your Colab notebook or local setup:

```python
# Install required libraries
!pip install --quiet --upgrade diffusers transformers accelerate mediapy

## Usage

Follow these steps to generate images from text:

### Import Libraries:

```python
import mediapy as media
import random
import sys
import torch
from diffusers import AutoPipelineForText2Image

Load the Pretrained Model:
python
Copy code
pipe = AutoPipelineForText2Image.from_pretrained(
    "stabilityai/sdxl-turbo",
    torch_dtype=torch.float16,
    use_safetensors=True,
    variant="fp16",
)
pipe = pipe.to("cuda")
Set Up Prompt and Seed:
python
Copy code
prompt = "a drunk guy"
seed = random.randint(0, sys.maxsize)
Generate Images:
python
Copy code
num_inference_steps = 4
images = pipe(
    prompt=prompt,
    guidance_scale=0.0,
    num_inference_steps=num_inference_steps,
    generator=torch.Generator("cuda").manual_seed(seed),
).images
Display and Save Image:
python
Copy code
print(f"Prompt:\t{prompt}\nSeed:\t{seed}")
media.show_images(images)
images[0].save("output.jpg")
Key Components
Diffusers Library: Simplifies working with diffusion models for tasks like text-to-image generation.
Model and Pipeline: Utilizes AutoPipelineForText2Image to load a pretrained model optimized for text-to-image generation.
Text Prompt and Seed: Allows specification of the textual description and ensures reproducibility with a random seed.
Inference Parameters:
num_inference_steps: Number of steps the model takes to generate an image.
guidance_scale: Controls the adherence to the text prompt.
GPU Acceleration: Moves the model to GPU (cuda) for faster computation.
Practical Applications
Art and Design: Generate unique visual content based on textual descriptions.
Content Creation: Automatically create images for blogs, articles, or social media posts.
Prototyping: Quickly generate visuals for concept art or storyboarding in creative industries.
