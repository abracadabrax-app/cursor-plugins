---
name: abracadabrax-product-photo-generator
description: "Use when the user asks for store-ready product shots. Turn a product description into a white-background packshot, a lifestyle scene, a flat lay, a hero banner or a close-up for a store or an ad, rendered in your Abracadabrax account. Uses the Abracadabrax tools of this plugin to prepare a draft, show its credit price, render it after the user confirms and return the file link."
---

# Abracadabrax AI Product Photo Generator

## When to use

Use when the user asks for store-ready product shots. Turn a product description into a white-background packshot, a lifestyle scene, a flat lay, a hero banner or a close-up for a store or an ad, rendered in your Abracadabrax account.

## What to ask for

Collect a description of the product, the kind of shot (white background, lifestyle, flat lay, hero banner, close-up) and any setting.

## Build the draft

- `tab`: `image`.
- `prompt` by kind of shot, always ending with `No text, no logos, no watermark.`:
  - white background (default): `Professional e-commerce product photo of <product> on a pure white seamless background, centered, soft even studio lighting, subtle natural shadow, sharp focus, true-to-life colors.`
  - lifestyle: `Lifestyle product photo of <product> in use in a real setting, natural light, shallow depth of field, authentic and aspirational. Setting: <setting>.`
  - flat lay: `Top-down flat lay product photo of <product> arranged with complementary props, soft diffused light, clean styling. Setting: <setting>.`
  - hero banner: `Wide hero banner product shot of <product>, dramatic studio lighting, premium advertising look, empty space on one side for a headline. Setting: <setting>.`
  - close-up: `Macro close-up product photo of <product> showing texture, materials and details, studio lighting, sharp focus.`
- `ratio`: `1:1` (default), `16:9` for a hero banner, or `4:3`, `3:4`, `9:16`.
- `model_id` (optional): `nano-banana-2` (default), `flux-2-pro`, `gpt-image-2`.

## Flow

1. Gather what the request needs (see above). Ask only for what is missing; sensible defaults are fine.
2. Call `prepare_media_project` with the arguments described above. It spends nothing.
3. Read the result back. `project.model_id`, `project.ratio` and `project.duration` are what will actually render: the server replaces an unknown model id with its default model, and a ratio or a length the model does not support with the model's default. If any of them differs from what the user asked for, say so and prepare again with a model that supports it.
4. Show the user the settings and `credits_required`, then wait for an explicit go-ahead. Skip the wait only when the user already asked you to generate.
5. Call `generate_media` with the `project_id`. This spends credits of the user's Abracadabrax account.
6. If the state is `insufficient_credits` or `account_required`, explain it and give the user the `dashboard_url` from the result. Never offer or sell credits or plans in the chat.
7. Call `get_media_job` with the `job_id` until the job is completed or failed, then give the user the absolute URL of the file so they can open or download it.

## Limits

Text only. Do not use this plugin for uploaded, attached or reference images or videos (editing, background removal, upscaling, image-to-video). For those, point the user to the Abracadabrax workspace at https://abracadabrax.app/workspace. Created from a description. It draws a new product image and does not edit, retouch or remove the background of a photo of your real product.
