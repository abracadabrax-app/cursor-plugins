---
name: abracadabrax-fantasy-map-generator
description: "Use when the user asks for maps of imaginary worlds. Create a map of an imaginary world, continent, kingdom, island, city or dungeon for your tabletop campaign, novel or game, with the place names you choose, rendered in your Abracadabrax account. Uses the Abracadabrax tools of this plugin to prepare a draft, show its credit price, render it after the user confirms and return the file link."
---

# Abracadabrax Fantasy Map Generator

## When to use

Use when the user asks for maps of imaginary worlds. Create a map of an imaginary world, continent, kingdom, island, city or dungeon for your tabletop campaign, novel or game, with the place names you choose, rendered in your Abracadabrax account.

## What to ask for

Collect the kind of map, the place and its geography, the names to label, the style and the format.

## Build the draft

- `tab`: `image`.
- `prompt`: `Top-down fantasy map of a <world|continent|kingdom|island|city|dungeon>: <geography>.` (default kingdom), then `Room-and-corridor dungeon floor plan with doors and stairs.` for a dungeon or `Coastlines, terrain, rivers, forests and settlements clearly drawn.` otherwise, then `Label these places on the map, spelled exactly: <names>. No other text.` or `No text labels.`, `Style: <style>.` (default: hand-drawn ink on aged parchment with a compass rose) and `The map fills the whole image, no frame around the image, no watermark.`
- `ratio`: `16:9` landscape (default), `1:1` or `3:4`.
- `model_id`: `nano-banana-pro` (default, readable labels), `nano-banana-2`, `gpt-image-2`.

## Flow

1. Gather what the request needs (see above). Ask only for what is missing; sensible defaults are fine.
2. Call `prepare_media_project` with the arguments described above. It spends nothing.
3. Read the result back. `project.model_id`, `project.ratio` and `project.duration` are what will actually render: the server replaces an unknown model id with its default model, and a ratio or a length the model does not support with the model's default. If any of them differs from what the user asked for, say so and prepare again with a model that supports it.
4. Show the user the settings and `credits_required`, then wait for an explicit go-ahead. Skip the wait only when the user already asked you to generate.
5. Call `generate_media` with the `project_id`. This spends credits of the user's Abracadabrax account.
6. If the state is `insufficient_credits` or `account_required`, explain it and give the user the `dashboard_url` from the result. Never offer or sell credits or plans in the chat.
7. Call `get_media_job` with the `job_id` until the job is completed or failed, then give the user the absolute URL of the file so they can open or download it.

## Limits

Text only. Do not use this plugin for uploaded, attached or reference images or videos (editing, background removal, upscaling, image-to-video). For those, point the user to the Abracadabrax workspace at https://abracadabrax.app/workspace. Imaginary places from text only. It does not map real places, provide navigation, or edit an uploaded map.
Original designs only. Do not use it for copyrighted characters, existing franchises, brand logos, trademarks or real celebrities; offer the user an original alternative instead.
