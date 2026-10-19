---
name: abracadabrax-pixel-art-generator
description: "Use when the user asks for pixel art and game sprites. Create 8-bit or 16-bit pixel art for indie games and posts: a character sprite, a sprite sheet, items and icons, a tileset or a full scene, rendered in your Abracadabrax account. Uses the Abracadabrax tools of this plugin to prepare a draft, show its credit price, render it after the user confirms and return the file link."
---

# Abracadabrax Pixel Art & Game Sprite Generator

## When to use

Use when the user asks for pixel art and game sprites. Create 8-bit or 16-bit pixel art for indie games and posts: a character sprite, a sprite sheet, items and icons, a tileset or a full scene, rendered in your Abracadabrax account.

## What to ask for

Collect what to draw, whether it is a character, a sprite sheet, items, tiles or a scene, 8-bit or 16-bit style and the palette.

## Build the draft

- `tab`: `image`.
- `prompt`: `Pixel art, <bit style>. <kind line>: <subject>.` then `Palette: <palette>.` when given and `Crisp hard-edged square pixels on a visible pixel grid, no anti-aliasing, no blur, no gradients, original design, no text, no watermark.`
  - bit style: `16-bit style with a richer palette` (default) or `8-bit retro style with a very limited palette`
  - character (default, `1:1`): `A single game character sprite, front-facing, centered on a plain flat background`
  - sprite sheet (`16:9`): `A sprite sheet of the same character in a row of animation frames (idle, walk, jump, attack), evenly spaced on a plain flat background`
  - items (`1:1`): `A grid of game items and icons, evenly spaced on a plain flat background`
  - tiles (`1:1`): `A tileset of seamless square terrain tiles arranged in a grid`
  - scene (`16:9`): `A complete game scene or level background`
- The image has a solid background, not a transparent one.
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

Text only. Do not use this plugin for uploaded, attached or reference images or videos (editing, background removal, upscaling, image-to-video). For those, point the user to the Abracadabrax workspace at https://abracadabrax.app/workspace. New pixel art from text only. It does not convert uploaded photos, export animated GIFs or game-engine files, or copy characters from existing games.
Original designs only. Do not use it for copyrighted characters, existing franchises, brand logos, trademarks or real celebrities; offer the user an original alternative instead.
