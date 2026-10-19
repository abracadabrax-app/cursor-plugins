---
name: abracadabrax-video-image-generation
description: "The user wants a new image or a short video clip created from a text description, and has not said which one, or wants both. Uses the Abracadabrax tools of this plugin to prepare a draft, show its credit price, render it after the user confirms and return the file link."
---

# Abracadabrax AI Image & Video Generator

## When to use

The user wants a new image or a short video clip created from a text description, and has not said which one, or wants both.

## What to ask for

Collect what the image or the clip shows (subject, setting, style, lighting), whether it is an image or a video, the aspect ratio and, for a video, the length.

## Build the draft

- `tab`: `image` or `video`.
- `prompt`: the full description, up to 3,000 characters. Put any text that must appear on the image in quotes and say it must be spelled exactly.
- `ratio`: for example `1:1`, `16:9`, `9:16`, `4:3`, `3:4`.
- `model_id` (optional): image models include `nano-banana-2` (default), `nano-banana-pro` (best for text on the image), `gpt-image-2` and `flux-2-pro`; video models include `kling-3-pro` (default), `sora-2` and `veo-3-1`.
- `duration` (video only): seconds, one of the lengths the model supports.

**Aspect ratios.** `2:3`, `3:2` and `21:9` work only on `nano-banana-2`, `nano-banana-pro` and `flux-2-pro`. On other image models (for example `gpt-image-2`) the server silently replaces them with the model's default ratio. Every image model takes `1:1`, `3:4`, `4:3`, `9:16` and `16:9`.

**Video formats and lengths.** `kling-3-pro` (default) takes `16:9`, `9:16` or `1:1` and 5 or 10 seconds. `sora-2` takes `16:9` or `9:16` and 4, 8 or 12 seconds. `veo-3-1` takes `16:9` or `9:16` and 4, 6 or 8 seconds. A format or a length the model does not support is silently replaced with the model's default.

## Flow

1. Gather what the request needs (see above). Ask only for what is missing; sensible defaults are fine.
2. Call `prepare_media_project` with `tab`, `prompt` and, when needed, `ratio`, `model_id` and `duration`. It spends nothing.
3. Read the result back. `project.model_id`, `project.ratio` and `project.duration` are what will actually render: the server replaces an unknown model id with its default model, and a ratio or a length the model does not support with the model's default. If any of them differs from what the user asked for, say so and prepare again with a model that supports it.
4. Show the user the settings and `credits_required`, then wait for an explicit go-ahead. Skip the wait only when the user already asked you to generate.
5. Call `generate_media` with the `project_id`. This spends credits of the user's Abracadabrax account.
6. If the state is `insufficient_credits` or `account_required`, explain it and give the user the `dashboard_url` from the result. Never offer or sell credits or plans in the chat.
7. Call `get_media_job` with the `job_id` until the job is completed or failed, then give the user the absolute URL of the file so they can open or download it.

## Limits

Text only. Do not use this plugin for uploaded, attached or reference images or videos (editing, background removal, upscaling, image-to-video). For those, point the user to the Abracadabrax workspace at https://abracadabrax.app/workspace.
