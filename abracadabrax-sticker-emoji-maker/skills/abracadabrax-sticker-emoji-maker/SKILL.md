---
name: abracadabrax-sticker-emoji-maker
description: "Use when the user asks for custom stickers and emoji. Create a custom die-cut sticker or emoji-style icon, one design or a set of 4, 6 or 9, with optional short text, on a plain background ready to cut out, rendered in your Abracadabrax account. Uses the Abracadabrax tools of this plugin to prepare a draft, show its credit price, render it after the user confirms and return the file link."
---

# Abracadabrax Sticker & Emoji Maker

## When to use

Use when the user asks for custom stickers and emoji. Create a custom die-cut sticker or emoji-style icon, one design or a set of 4, 6 or 9, with optional short text, on a plain background ready to cut out, rendered in your Abracadabrax account.

## What to ask for

Collect what the sticker or emoji shows, whether it is a die-cut sticker or an emoji, how many designs (1, 4, 6 or 9), any short text and the style.

## Build the draft

- `tab`: `image`.
- `ratio`: `1:1`.
- `prompt`: for one design `Die-cut sticker with a thick white border following the outline of the design: <subject>.` (or `Emoji-style icon, simple and readable at a very small size: <subject>.`); for a set of 4, 6 or 9 `A set of <n> different <die-cut stickers|emoji-style icons> on the theme "<subject>", evenly spaced in a grid, each one separate.` Then `Style: <style>.` (default: cute, bold cartoon with clean outlines), `Text on the sticker, spelled exactly: "<text>".` (up to 30 characters) or `No text.`, and `Plain flat <color> background, no shadows on the background, no mockup, no watermark.` (default white). The image has a solid background, not a transparent one.
- `model_id`: `nano-banana-2` (default), `nano-banana-pro` (better text), `gpt-image-2`.

## Flow

1. Gather what the request needs (see above). Ask only for what is missing; sensible defaults are fine.
2. Call `prepare_media_project` with the arguments described above. It spends nothing.
3. Read the result back. `project.model_id`, `project.ratio` and `project.duration` are what will actually render: the server replaces an unknown model id with its default model, and a ratio or a length the model does not support with the model's default. If any of them differs from what the user asked for, say so and prepare again with a model that supports it.
4. Show the user the settings and `credits_required`, then wait for an explicit go-ahead. Skip the wait only when the user already asked you to generate.
5. Call `generate_media` with the `project_id`. This spends credits of the user's Abracadabrax account.
6. If the state is `insufficient_credits` or `account_required`, explain it and give the user the `dashboard_url` from the result. Never offer or sell credits or plans in the chat.
7. Call `get_media_job` with the `job_id` until the job is completed or failed, then give the user the absolute URL of the file so they can open or download it.

## Limits

Text only. Do not use this plugin for uploaded, attached or reference images or videos (editing, background removal, upscaling, image-to-video). For those, point the user to the Abracadabrax workspace at https://abracadabrax.app/workspace. New stickers from text only. It does not turn uploaded photos into stickers, copy brand or copyrighted characters, or send stickers to messaging apps.
Original designs only. Do not use it for copyrighted characters, existing franchises, brand logos, trademarks or real celebrities; offer the user an original alternative instead.
