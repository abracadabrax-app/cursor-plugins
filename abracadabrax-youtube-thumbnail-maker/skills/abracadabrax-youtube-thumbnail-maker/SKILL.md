---
name: abracadabrax-youtube-thumbnail-maker
description: "Use when the user asks for bold 16:9 video thumbnails. Design a bold 16:9 video thumbnail from the topic of your video and a short headline, rendered in your Abracadabrax account. Uses the Abracadabrax tools of this plugin to prepare a draft, show its credit price, render it after the user confirms and return the file link."
---

# Abracadabrax YouTube Thumbnail Maker

## When to use

Use when the user asks for bold 16:9 video thumbnails. Design a bold 16:9 video thumbnail from the topic of your video and a short headline, rendered in your Abracadabrax account.

## What to ask for

Collect the video topic, an optional headline of 2-6 words, the main subject and the style.

## Build the draft

- `tab`: `image`.
- `ratio`: `16:9`.
- `model_id`: `nano-banana-pro` unless the user picks another (it renders text most sharply).
- `prompt`, in this order: `YouTube thumbnail, 16:9, for a video about <topic>.` `Main subject: <subject>.` then either `Large bold headline text that reads exactly "<headline>", readable at small size.` (headline of 2-6 words) or `No text on the image.`, then `Style: <style>.` (default: bold, high contrast, vibrant, expressive, clean composition with one clear focal point) and `Color palette: <colors>.` when given.

## Flow

1. Gather what the request needs (see above). Ask only for what is missing; sensible defaults are fine.
2. Call `prepare_media_project` with the arguments described above. It spends nothing.
3. Read the result back. `project.model_id`, `project.ratio` and `project.duration` are what will actually render: the server replaces an unknown model id with its default model, and a ratio or a length the model does not support with the model's default. If any of them differs from what the user asked for, say so and prepare again with a model that supports it.
4. Show the user the settings and `credits_required`, then wait for an explicit go-ahead. Skip the wait only when the user already asked you to generate.
5. Call `generate_media` with the `project_id`. This spends credits of the user's Abracadabrax account.
6. If the state is `insufficient_credits` or `account_required`, explain it and give the user the `dashboard_url` from the result. Never offer or sell credits or plans in the chat.
7. Call `get_media_job` with the `job_id` until the job is completed or failed, then give the user the absolute URL of the file so they can open or download it.

## Limits

Text only. Do not use this plugin for uploaded, attached or reference images or videos (editing, background removal, upscaling, image-to-video). For those, point the user to the Abracadabrax workspace at https://abracadabrax.app/workspace. New designs from text only. It does not put your own photo or face on the thumbnail or edit an existing one.
