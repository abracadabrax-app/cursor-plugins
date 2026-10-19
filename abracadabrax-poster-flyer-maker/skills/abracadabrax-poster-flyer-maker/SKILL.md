---
name: abracadabrax-poster-flyer-maker
description: "Use when the user asks for posters and flyers with text. Design a print-ready poster or flyer with the headline and the details of your event, sale or announcement laid out on it, rendered in your Abracadabrax account. Uses the Abracadabrax tools of this plugin to prepare a draft, show its credit price, render it after the user confirms and return the file link."
---

# Abracadabrax Poster & Flyer Maker

## When to use

Use when the user asks for posters and flyers with text. Design a print-ready poster or flyer with the headline and the details of your event, sale or announcement laid out on it, rendered in your Abracadabrax account.

## What to ask for

Collect the kind of poster or flyer, the headline, the details to print (date, place, offer) and the visual theme.

## Build the draft

- `tab`: `image`.
- `prompt`: `Design a <kind> with the headline "<headline>" in large typography, spelled exactly as written.` (kind: event poster, flyer, sale flyer, concert poster, movie poster or announcement), then `Smaller secondary text, spelled exactly: "<details>".` for date, time, place or offer, `Visual theme: <theme>.` (default: modern, bold and eye-catching) and `Clear visual hierarchy, balanced layout, print-ready, no other text.`
- `ratio`: `2:3` portrait (default), `1:1` square or `3:2` landscape.
- `model_id`: `nano-banana-pro` (default, sharp text) or `nano-banana-2`.

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

Text only. Do not use this plugin for uploaded, attached or reference images or videos (editing, background removal, upscaling, image-to-video). For those, point the user to the Abracadabrax workspace at https://abracadabrax.app/workspace. Designs from text only. It does not place your own photos or logo files on the design, edit an existing poster file or print it.
