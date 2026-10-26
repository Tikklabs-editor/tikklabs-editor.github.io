---
title: "Can Local AI Replace Your Subscription? Start ComfyUI and Check Licenses"
date: 2026-03-31T16:00:00+09:00
lastmod: 2026-10-05T13:46:25+09:00
draft: false
authors: ["tikklabs-editor"]
categories: ["Local AI"]
tags: ["ComfyUI", "SDXL", "Local AI"]
slug: "it-productivity-local-ai-guide"
translationKey: "local-ai-guide"
featureimage: "img/editorial/local-ai.webp"
description: "Set up a first ComfyUI image workflow, troubleshoot common issues, and compare local costs and model licenses before cancelling subscriptions."
showToc: true
---

Before cancelling an image-generation subscription, test whether your existing PC can handle one repeatable job. Local AI runs a model on your computer. A fully local workflow can avoid per-generation cloud credits, but it still uses electricity, hardware and maintenance time.

This guide covers a first ComfyUI image workflow and a cost-and-license checklist. It does not provide measured performance claims for a particular GPU.

## Choose one workload to move first

| Situation | Starting point |
|---|---|
| Repeated backgrounds or illustrations; a suitable PC already available | Try local image generation for that task |
| Occasional use; little time for configuration | Free allowances or a subscription only when needed |
| Mixed image, voice and video work with tight deadlines | Combine local and hosted tools |
| Client or internal material | Check external API and upload behavior as well as the model |

Local images, text-to-speech and chat models are separate workloads. Installing an image tool does not automatically set up voice generation.

![Fully local processing versus external API processing](img/editorial/local-scope-en.svg "An explanatory diagram. A local application can still send data out when an external API is selected.")

## Start ComfyUI on Windows

1. Download through the [official Windows installation page](https://docs.comfy.org/installation/desktop/windows).
2. Install and launch Comfy Desktop, then create your first ComfyUI instance. Check available storage for models and outputs.
3. Open the [official SDXL Base model page](https://huggingface.co/stabilityai/stable-diffusion-xl-base-1.0) and review its license. This example uses `sd_xl_base_1.0.safetensors`.
4. Place the model in that instance's `models/checkpoints` directory. The full path depends on your installation location and Desktop version.
5. Load the basic flow from the [official text-to-image example](https://docs.comfy.org/tutorials/basic/text-to-image). Select SDXL Base in **Load Checkpoint**, rather than the SD1.5 model shown in that example.
6. Set **Empty Latent Image** to 1024×1024 and batch size to 1. Start without extra LoRAs or custom nodes.
7. Enter a prompt such as `a ceramic mug on a wooden desk, soft daylight, simple background`. Select **Queue** or press `Ctrl+Enter`.
8. Confirm that **Save Image** shows a result. Repeat a small test and record quality, time and revisions.

The [official SDXL examples](https://comfyanonymous.github.io/ComfyUI_examples/sdxl/) explain that the Base model works as a regular checkpoint. You do not need to add a Refiner for your first test.

## Troubleshoot the first run

| Problem | First check |
|---|---|
| Model missing from the selector | Check the active instance's checkpoints folder; refresh or restart |
| Out-of-memory error | Use batch size 1, close other GPU applications, and consider a lighter model |
| Missing nodes | Return to a basic workflow that does not require extra plugins |
| Unsatisfactory output | Change model, prompt or resolution individually and compare |

Application support is different from a model's hardware needs. Memory use depends on the model, resolution and concurrent tasks. Test your current machine before buying hardware for AI.

## A free download does not establish commercial permission

SDXL Base 1.0 uses **CreativeML Open RAIL++-M**, which includes use restrictions. Check separate terms for derivative checkpoints and LoRAs; not every Stable Diffusion model has identical terms.

For speech, **XTTS-v2's public license permits only non-commercial use of the model and its outputs**. It is not a blanket free recommendation for paid deliverables or revenue-generating content. Assess language support, quality and the actual model license together.

- [SDXL Base license](https://huggingface.co/stabilityai/stable-diffusion-xl-base-1.0/blob/main/LICENSE.md)
- [XTTS-v2 license](https://huggingface.co/coqui/XTTS-v2/blob/main/LICENSE.txt)

## Compare usable results before cancelling

**Monthly local cost = additional electricity + allocated hardware cost + actual maintenance expenses.**

Using a PC you already own differs from buying one specifically for AI. Also record time spent reaching an acceptable result. Compare the cost of a finished, usable image rather than the raw number generated.

Move one recurring job first. Reduce the subscription only when local quality and turnaround meet your needs, keeping hosted tools for work that is harder to replace.

Documentation and license check: October 5, 2026.

[Related guide: Verify AI answers before using them](/post/stone-age-brain-vs-gpt/)

[Start with the topic guides](/guides/)
