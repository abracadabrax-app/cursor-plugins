---
name: abracadabrax-ai-character-generator
description: "Use when the user asks for original game and story heroes. Design an original character for a fantasy or RPG campaign, a video game, a story or a mascot, as a portrait, a full-body figure or a character sheet, rendered in your Abracadabrax account. Uses the Abracadabrax tools of this plugin to prepare a draft, show its credit price, render it after the user confirms and return the file link."
---

# Abracadabrax AI Character Generator

## When to use

Use when the user asks for original game and story heroes. Design an original character for a fantasy or RPG campaign, a video game, a story or a mascot, as a portrait, a full-body figure or a character sheet, rendered in your Abracadabrax account.

## What to ask for

Collect who the character is and how they look, the setting or genre, the view (portrait, full body or character sheet) and the art style.

## Build the draft

- `tab`: `image`.
- `prompt`: `Original character design: <character>.` `Setting: <world>.` then the view line, `Art style: <style>.` (default: detailed painterly fantasy illustration) and `Original design, not based on any existing franchise character. Plain neutral background, no text, no watermark.`
  - portrait (default, `3:4`): `Head-and-shoulders character portrait.`
  - full body (`3:4`): `Full-body character in a clear standing pose, the whole figure in frame.`
  - character sheet (`16:9`): `Character reference sheet: the same character shown from the front, the side and the back, side by side, with a consistent design.`
- `model_id`: `nano-banana-pro` (default), `nano-banana-2`, `gpt-image-2`, `flux-2-pro`.

## Flow

1. Gather what the request needs (see above). Ask only for what is missing; sensible defaults are fine.
2. Call `prepare_media_project` with the arguments described above. It spends nothing.
3. Read the result back. `project.model_id`, `project.ratio` and `project.duration` are what will actually render: the server replaces an unknown model id with its default model, and a ratio or a length the model does not support with the model's default. If any of them differs from what the user asked for, say so and prepare again with a model that supports it.
4. Show the user the settings and `credits_required`, then wait for an explicit go-ahead. Skip the wait only when the user already asked you to generate.
5. Call `generate_media` with the `project_id`. This spends credits of the user's Abracadabrax account.
6. If the state is `insufficient_credits` or `account_required`, explain it and give the user the `dashboard_url` from the result. Never offer or sell credits or plans in the chat.
7. Call `get_media_job` with the `job_id` until the job is completed or failed, then give the user the absolute URL of the file so they can open or download it.

## Limits

Text only. Do not use this plugin for uploaded, attached or reference images or videos (editing, background removal, upscaling, image-to-video). For those, point the user to the Abracadabrax workspace at https://abracadabrax.app/workspace. Original characters from text only. It does not draw copyrighted or existing characters or real people, and it does not edit uploaded images.
Original designs only. Do not use it for copyrighted characters, existing franchises, brand logos, trademarks or real celebrities; offer the user an original alternative instead.
