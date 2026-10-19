---
name: abracadabrax-social-media-image
description: "Use when the user asks for post images sized per platform. Turn a post idea into an image sized for Instagram, Facebook, LinkedIn, X, Pinterest or a vertical story, with optional text and brand colors, rendered in your Abracadabrax account. Uses the Abracadabrax tools of this plugin to prepare a draft, show its credit price, render it after the user confirms and return the file link."
---

# Abracadabrax Social Media Image & Post Maker

## When to use

Use when the user asks for post images sized per platform. Turn a post idea into an image sized for Instagram, Facebook, LinkedIn, X, Pinterest or a vertical story, with optional text and brand colors, rendered in your Abracadabrax account.

## What to ask for

Collect the platform, what the image shows, any text to print on it and the style or brand colors.

## Build the draft

- `tab`: `image`.
- `ratio` by platform: Instagram post, Facebook post and LinkedIn post `1:1`; Instagram portrait `3:4`; story or reel cover `9:16`; X post `16:9`; Pinterest pin `2:3`.
- `prompt`: `<platform> image: <idea>.` then `Text on the image, spelled exactly: "<text>".` (up to about 80 characters) or `No text on the image.`, then `Style: <style>.` (default: scroll-stopping composition, crisp details) and `Brand colors: <colors>.` when given.
- `model_id` (optional): `nano-banana-2` (default), `nano-banana-pro` (better text), `gpt-image-2`, `flux-2-pro`.

**Aspect ratios.** `2:3`, `3:2` and `21:9` work only on `nano-banana-2`, `nano-banana-pro` and `flux-2-pro`. On other image models (for example `gpt-image-2`) the server silently replaces them with the model's default ratio. Every image model takes `1:1`, `3:4`, `4:3`, `9:16` and `16:9`.

## Flow

1. Gather what the request needs (see above). Ask only for what is missing; sensible defaults are fine.
2. Call `prepare_media_project` with the arguments described above. It spends nothing.
3. Read the result back. `project.model_id`, `project.ratio` and `project.duration` are what will actually render: the server replaces an unknown model id with its default model, and a ratio or a length the model does not support with the model's default. If any of them differs from what the user asked for, say so and prepare again with a model that supports it.
4. Show the user the settings and `credits_required`, then wait for an explicit go-ahead. Skip the wait only when the user already asked you to generate.
5. Call `generate_media` with the `project_id`. This spends credits of the user's Abracadabrax account.
6. If the state is `insufficient_credits` or `account_required`, explain it and give the user the `dashboard_url` from the result. Never offer or sell credits or plans in the chat.
7. Call `get_media_job` with the `job_id` until the job is completed or failed, then give the user the absolute URL of the file so they can open or download it.

## Limits

Text only. Do not use this plugin for uploaded, attached or reference images or videos (editing, background removal, upscaling, image-to-video). For those, point the user to the Abracadabrax workspace at https://abracadabrax.app/workspace. New images only. It does not edit photos you already have, add your logo file, or publish or schedule posts.
