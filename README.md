---
license: other
license_name: playground-v2-community
license_link: https://huggingface.co/playgroundai/playground-v2-1024px-aesthetic/blob/main/LICENSE.md
tags:
- text-to-image
- playground
---
# Playground v2 – 1024px Aesthetic Model

This repository contains a model that generates highly aesthetic images of resolution 1024x1024. You can use the model with Hugging Face 🧨 Diffusers.

<div>
  <div style="display: flex; flex-direction: row; width: 100%;">
    <img style="margin: 0; max-width: 33%; object-fit: scale-down; flex-shrink: 1;" src="https://cdn-uploads.huggingface.co/production/uploads/63855d851769b7c4b10e1f76/GBZVS0a4QcRY4eVBCExFK.jpeg" />
    <img style="margin: 0; max-width: 33%; object-fit: scale-down; flex-shrink: 1;" src="https://cdn-uploads.huggingface.co/production/uploads/63855d851769b7c4b10e1f76/iqGvvAdz2TqV0G3p9zOXZ.png" />
    <img style="margin: 0; max-width: 33%; object-fit: scale-down; flex-shrink: 1;" src="https://cdn-uploads.huggingface.co/production/uploads/63855d851769b7c4b10e1f76/2_BMfgFVXUoU-0ocsOz0M.png" />
  </div>
  <div style="display: flex; flex-direction: row; width: 100%;">
    <img style="margin: 0; max-width: 33%; object-fit: scale-down; flex-shrink: 1;" src="https://cdn-uploads.huggingface.co/production/uploads/63855d851769b7c4b10e1f76/-a4tx6c9EMc88fmchW0nG.png" />
    <img style="margin: 0; max-width: 33%; object-fit: scale-down; flex-shrink: 1;" src="https://cdn-uploads.huggingface.co/production/uploads/63855d851769b7c4b10e1f76/LKCjxb9NoqfRtcviaEILI.png" />
    <img style="margin: 0; max-width: 33%; object-fit: scale-down; flex-shrink: 1;" src="https://cdn-uploads.huggingface.co/production/uploads/63855d851769b7c4b10e1f76/cRSItLGH42V2kz9pM6huZ.png" />
  </div>
</div>

**Playground v2** is a diffusion-based text-to-image generative model. The model was trained from scratch by the research team at [Playground](https://playground.com). 

Playground v2’s images are favored **2.5** times more than those produced by Stable Diffusion XL, according to Playground’s [user study](#user-study).

We are thrilled to release [intermediate checkpoints](#intermediate-base-models) at different training stages, including evaluation metrics, to the community. We hope this will foster more foundation model research in pixels.

Lastly, we introduce a new benchmark, [MJHQ-30K](#mjhq-30k-benchmark), for automatic evaluation of a model’s aesthetic quality.

### Model Description

- **Developed by:** [Playground](https://playground.com)
- **Model type:** Diffusion-based text-to-image generative model
- **License:** [Playground v2 Community License](https://huggingface.co/playgroundai/playground-v2-1024px-aesthetic/blob/main/LICENSE.md)
- **Model Description:** This model generates images based on text prompts. It is a Latent Diffusion Model that uses two fixed, pre-trained text encoders ([OpenCLIP-ViT/G](https://github.com/mlfoundations/open_clip) and [CLIP-ViT/L](https://github.com/openai/CLIP/tree/main)). It follows the same architecture as [Stable Diffusion XL](https://huggingface.co/stabilityai/stable-diffusion-xl-base-1.0).

### Using the model with 🧨 Diffusers

Install diffusers >= 0.24.0 and some dependencies:
```
pip install transformers accelerate safetensors
```

To use the model, run:

```python
from diffusers import DiffusionPipeline
import torch

pipe = DiffusionPipeline.from_pretrained(
    "playgroundai/playground-v2-1024px-aesthetic",
    torch_dtype=torch.float16,
    use_safetensors=True,
    add_watermarker=False,
    variant="fp16"
)
pipe.to("cuda")

prompt = "Astronaut in a jungle, cold color palette, muted colors, detailed, 8k"
image  = pipe(prompt=prompt).images[0]
```

### User Study

![image/png](https://cdn-uploads.huggingface.co/production/uploads/63855d851769b7c4b10e1f76/8VzBkSYaUU3dt509Co9sk.png)

According to user studies conducted by Playground, involving over 2,600 prompts and thousands of users, the images generated by Playground v2 are favored **2.5** times more than those produced by [Stable Diffusion XL](https://huggingface.co/stabilityai/stable-diffusion-xl-base-1.0).

We report user preference metrics on [PartiPrompts](https://github.com/google-research/parti), following standard practice, and on an internal prompt dataset curated by the Playground team. The “Internal 1K” prompt dataset is diverse and covers various categories and tasks.

During the user study, we give users instructions to evaluate image pairs based on both (1) their aesthetic preference and (2) the image-text alignment.

### MJHQ-30K Benchmark

![image/png](https://cdn-uploads.huggingface.co/production/uploads/63855d851769b7c4b10e1f76/o3Bt62qFsTO9DkeX2yLua.png)

| Model                                 | Overall FID   |
| ------------------------------------- | ----- |
| SDXL-1-0-refiner                      | 9.55  |
| [playground-v2-1024px-aesthetic](https://huggingface.co/playgroundai/playground-v2-1024px-aesthetic)        | **7.07**  |

We introduce a new benchmark, [MJHQ-30K](https://huggingface.co/datasets/playgroundai/MJHQ-30K), for automatic evaluation of a model’s aesthetic quality. The benchmark computes FID on a high-quality dataset to gauge aesthetic quality.

We curate the high-quality dataset from Midjourney with 10 common categories, each category with 3K samples. Following common practice, we use aesthetic score and CLIP score to ensure high image quality and high image-text alignment. Furthermore, we take extra care to make the data diverse within each category.

For Playground v2, we report both the overall FID and per-category FID. All FID metrics are computed at resolution 1024x1024. Our benchmark results show that our model outperforms SDXL-1-0-refiner in overall FID and all category FIDs, especially in people and fashion categories. This is in line with the results of the user study, which indicates a correlation between human preference and FID score on the MJHQ-30K benchmark.

We release this benchmark to the public and encourage the community to adopt it for benchmarking their models’ aesthetic quality.

### Intermediate Base Models

| Model                        | FID    | Clip Score |
| ---------------------------- | ------ | ---------- |
| SDXL-1-0-refiner             | 13.04  | 32.62      |
| [playground-v2-256px-base](https://huggingface.co/playgroundai/playground-v2-256px-base)     | 9.83   | 31.90      |
| [playground-v2-512px-base](https://huggingface.co/playgroundai/playground-v2-512px-base)     | 9.55   | 32.08      |


Apart from [playground-v2-1024px-aesthetic](https://huggingface.co/playgroundai/playground-v2-1024px-aesthetic), we release intermediate checkpoints at different training stages to the community in order to foster foundation model research in pixels. Here, we report the FID score and CLIP score on the MSCOCO14 evaluation set for the reference purposes. (Note that our reported numbers may differ from the numbers reported in SDXL’s published results, as our prompt list may be different.)