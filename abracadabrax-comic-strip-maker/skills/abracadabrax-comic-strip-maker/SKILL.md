---
name: abracadabrax-comic-strip-maker
description: "Use when the user asks for comics with speech bubbles. Create an original comic strip of 3, 4 or 6 panels with speech bubbles from your story and characters, in cartoon, manga, newspaper or graphic novel style, rendered in your Abracadabrax account. Uses the Abracadabrax tools of this plugin to prepare a draft, show its credit price, render it after the user confirms and return the file link."
---

# Abracadabrax Comic Strip Maker

## When to use

Use when the user asks for comics with speech bubbles. Create an original comic strip of 3, 4 or 6 panels with speech bubbles from your story and characters, in cartoon, manga, newspaper or graphic novel style, rendered in your Abracadabrax account.

## What to ask for

Collect the story panel by panel with the dialogue, the characters and how they look, the number of panels (3, 4 or 6) and the style.

## Build the draft

- `tab`: `image`.
- `prompt`: `Original comic strip, <layout>, <style>.` `Characters, drawn the same way in every panel: <characters>.` `Story and dialogue: <story, panel by panel, with the dialogue>` and `Speech bubbles with the dialogue spelled exactly, clear panel borders, original characters only, no watermark.`
  - panels: 3 = `three panels in one horizontal row` (`16:9`); 4 (default) = `four panels in a two-by-two grid` (`1:1`); 6 = `six panels in a grid of three rows of two` (`3:4`)
  - style: `colorful cartoon style` (default), `black-and-white manga style with screentones`, `classic newspaper comic strip style` or `detailed graphic novel style with dramatic lighting`
- `model_id`: `nano-banana-pro` (default, readable bubbles), `gpt-image-2`, `nano-banana-2`.

## Flow

1. Gather what the request needs (see above). Ask only for what is missing; sensible defaults are fine.
2. Call `prepare_media_project` with the arguments described above. It spends nothing.
3. Read the result back. `project.model_id`, `project.ratio` and `project.duration` are what will actually render: the server replaces an unknown model id with its default model, and a ratio or a length the model does not support with the model's default. If any of them differs from what the user asked for, say so and prepare again with a model that supports it.
4. Show the user the settings and `credits_required`, then wait for an explicit go-ahead. Skip the wait only when the user already asked you to generate.
5. Call `generate_media` with the `project_id`. This spends credits of the user's Abracadabrax account.
6. If the state is `insufficient_credits` or `account_required`, explain it and give the user the `dashboard_url` from the result. Never offer or sell credits or plans in the chat.
7. Call `get_media_job` with the `job_id` until the job is completed or failed, then give the user the absolute URL of the file so they can open or download it.

## Limits

Text only. Do not use this plugin for uploaded, attached or reference images or videos (editing, background removal, upscaling, image-to-video). For those, point the user to the Abracadabrax workspace at https://abracadabrax.app/workspace. Original strips from text only. It does not use copyrighted characters or real people, and it does not edit uploaded comics.
Original designs only. Do not use it for copyrighted characters, existing franchises, brand logos, trademarks or real celebrities; offer the user an original alternative instead.
