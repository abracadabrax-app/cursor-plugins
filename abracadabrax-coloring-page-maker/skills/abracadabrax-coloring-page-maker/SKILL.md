---
name: abracadabrax-coloring-page-maker
description: "Use when the user asks for printable coloring pages. Draw a printable black-and-white coloring page from a subject or a scene, simple for toddlers, detailed for kids or intricate for adults, rendered in your Abracadabrax account. Uses the Abracadabrax tools of this plugin to prepare a draft, show its credit price, render it after the user confirms and return the file link."
---

# Abracadabrax Coloring Page Maker

## When to use

Use when the user asks for printable coloring pages. Draw a printable black-and-white coloring page from a subject or a scene, simple for toddlers, detailed for kids or intricate for adults, rendered in your Abracadabrax account.

## What to ask for

Collect what to draw, who will color it (toddler, kids or adults), a plain or scene background and the page format.

## Build the draft

- `tab`: `image`.
- `prompt`: `Printable coloring book page: <subject>.` `Black and white line art only: pure black outlines on a pure white background, no shading, no gray tones, no color, no filled areas, closed shapes ready to color.` then the level line, the background line and `No text, no border frame, no watermark.`
  - toddler: `Very simple shapes with thick bold outlines and large areas to color, for toddlers aged 2 to 4.`
  - kids (default): `Clear medium-thick outlines with a moderate amount of detail, for children aged 5 to 10.`
  - adults: `Intricate, detailed line work with fine lines and patterns, for adult coloring.`
  - background: `Plain white background around the subject.` (default) or `A simple background scene drawn in the same line art style.`
- `ratio`: `3:4` portrait (default), `4:3` landscape or `1:1`.
- `model_id`: `nano-banana-2` (default), `gpt-image-2`, `nano-banana-pro`.

## Flow

1. Gather what the request needs (see above). Ask only for what is missing; sensible defaults are fine.
2. Call `prepare_media_project` with the arguments described above. It spends nothing.
3. Read the result back. `project.model_id`, `project.ratio` and `project.duration` are what will actually render: the server replaces an unknown model id with its default model, and a ratio or a length the model does not support with the model's default. If any of them differs from what the user asked for, say so and prepare again with a model that supports it.
4. Show the user the settings and `credits_required`, then wait for an explicit go-ahead. Skip the wait only when the user already asked you to generate.
5. Call `generate_media` with the `project_id`. This spends credits of the user's Abracadabrax account.
6. If the state is `insufficient_credits` or `account_required`, explain it and give the user the `dashboard_url` from the result. Never offer or sell credits or plans in the chat.
7. Call `get_media_job` with the `job_id` until the job is completed or failed, then give the user the absolute URL of the file so they can open or download it.

## Limits

Text only. Do not use this plugin for uploaded, attached or reference images or videos (editing, background removal, upscaling, image-to-video). For those, point the user to the Abracadabrax workspace at https://abracadabrax.app/workspace. Pages from text only. It does not turn your own photo or drawing into a coloring page or color it in.
