---
name: abracadabrax-ai-wallpaper-maker
description: "Use when the user asks for phone and desktop wallpapers. Create a wallpaper from a theme and a style, sized for phone, desktop, tablet or a square screen with space kept clear for icons and the clock, rendered in your Abracadabrax account. Uses the Abracadabrax tools of this plugin to prepare a draft, show its credit price, render it after the user confirms and return the file link."
---

# Abracadabrax AI Wallpaper Maker

## When to use

Use when the user asks for phone and desktop wallpapers. Create a wallpaper from a theme and a style, sized for phone, desktop, tablet or a square screen with space kept clear for icons and the clock, rendered in your Abracadabrax account.

## What to ask for

Collect the theme of the wallpaper, the device (phone, desktop, tablet or square), the style and any color palette.

## Build the draft

- `tab`: `image`.
- `prompt`: the device line, then `: <theme>.`, `Style: <style>.` (default: high-detail, cinematic and atmospheric), `Color palette: <colors>.` when given, and `Sharp, high resolution, edge-to-edge composition, no text, no logo, no watermark.`
  - phone (default, `9:16`): `Vertical phone wallpaper, keep the top third calm and uncluttered for the clock and the main subject in the lower two thirds`
  - desktop (`16:9`): `Widescreen desktop wallpaper, keep the left side calmer for desktop icons`
  - tablet (`4:3`): `Tablet wallpaper with a balanced composition`
  - square (`1:1`): `Square wallpaper with a balanced composition`
- `model_id`: `nano-banana-2` (default), `nano-banana-pro`, `flux-2-pro`.

## Flow

1. Gather what the request needs (see above). Ask only for what is missing; sensible defaults are fine.
2. Call `prepare_media_project` with the arguments described above. It spends nothing.
3. Read the result back. `project.model_id`, `project.ratio` and `project.duration` are what will actually render: the server replaces an unknown model id with its default model, and a ratio or a length the model does not support with the model's default. If any of them differs from what the user asked for, say so and prepare again with a model that supports it.
4. Show the user the settings and `credits_required`, then wait for an explicit go-ahead. Skip the wait only when the user already asked you to generate.
5. Call `generate_media` with the `project_id`. This spends credits of the user's Abracadabrax account.
6. If the state is `insufficient_credits` or `account_required`, explain it and give the user the `dashboard_url` from the result. Never offer or sell credits or plans in the chat.
7. Call `get_media_job` with the `job_id` until the job is completed or failed, then give the user the absolute URL of the file so they can open or download it.

## Limits

Text only. Do not use this plugin for uploaded, attached or reference images or videos (editing, background removal, upscaling, image-to-video). For those, point the user to the Abracadabrax workspace at https://abracadabrax.app/workspace. New wallpapers from text only. It does not resize, crop or restyle your own photos.
Original designs only. Do not use it for copyrighted characters, existing franchises, brand logos, trademarks or real celebrities; offer the user an original alternative instead.
