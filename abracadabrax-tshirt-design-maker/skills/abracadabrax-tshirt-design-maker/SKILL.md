---
name: abracadabrax-tshirt-design-maker
description: "Use when the user asks for prints for tees and hoodies. Create an original graphic and optional slogan for t-shirts, hoodies and print-on-demand merch, centered on a plain background in the color of the garment, rendered in your Abracadabrax account. Uses the Abracadabrax tools of this plugin to prepare a draft, show its credit price, render it after the user confirms and return the file link."
---

# Abracadabrax T-Shirt Design Maker

## When to use

Use when the user asks for prints for tees and hoodies. Create an original graphic and optional slogan for t-shirts, hoodies and print-on-demand merch, centered on a plain background in the color of the garment, rendered in your Abracadabrax account.

## What to ask for

Collect what the graphic shows, any slogan to print, the style, the garment color and the format.

## Build the draft

- `tab`: `image`.
- `prompt`: `Original t-shirt print graphic: <design>.` `Style: <style>.` (default: bold vector illustration with a limited color palette), `Text in the design, spelled exactly: "<slogan>". No other text.` or `No text.`, and `Centered on a solid flat <garment color> background that matches the garment color, print-ready, no shirt, no mockup, no brand logos, no watermark.` (default black). Not a transparent image.
- `ratio`: `3:4` front print (default) or `1:1` chest or pocket print.
- `model_id`: `nano-banana-pro` (default, sharp text), `gpt-image-2`, `nano-banana-2`, `flux-2-pro`.

## Flow

1. Gather what the request needs (see above). Ask only for what is missing; sensible defaults are fine.
2. Call `prepare_media_project` with the arguments described above. It spends nothing.
3. Read the result back. `project.model_id`, `project.ratio` and `project.duration` are what will actually render: the server replaces an unknown model id with its default model, and a ratio or a length the model does not support with the model's default. If any of them differs from what the user asked for, say so and prepare again with a model that supports it.
4. Show the user the settings and `credits_required`, then wait for an explicit go-ahead. Skip the wait only when the user already asked you to generate.
5. Call `generate_media` with the `project_id`. This spends credits of the user's Abracadabrax account.
6. If the state is `insufficient_credits` or `account_required`, explain it and give the user the `dashboard_url` from the result. Never offer or sell credits or plans in the chat.
7. Call `get_media_job` with the `job_id` until the job is completed or failed, then give the user the absolute URL of the file so they can open or download it.

## Limits

Text only. Do not use this plugin for uploaded, attached or reference images or videos (editing, background removal, upscaling, image-to-video). For those, point the user to the Abracadabrax workspace at https://abracadabrax.app/workspace. Original prints from text only. It does not copy brand logos or copyrighted characters, mock up the design on a photo, or place orders with print shops.
Original designs only. Do not use it for copyrighted characters, existing franchises, brand logos, trademarks or real celebrities; offer the user an original alternative instead.
