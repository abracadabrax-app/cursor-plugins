---
name: abracadabrax-album-cover-maker
description: "Use when the user asks for square art for music releases. Design square cover art for an album, single, EP, mixtape or playlist from the title, the artist, the genre and the mood, rendered in your Abracadabrax account. Uses the Abracadabrax tools of this plugin to prepare a draft, show its credit price, render it after the user confirms and return the file link."
---

# Abracadabrax Album Cover Art Maker

## When to use

Use when the user asks for square art for music releases. Design square cover art for an album, single, EP, mixtape or playlist from the title, the artist, the genre and the mood, rendered in your Abracadabrax account.

## What to ask for

Collect the title, the artist name, the genre, the mood, the visual style and whether the title is printed on the cover.

## Build the draft

- `tab`: `image`.
- `ratio`: `1:1`.
- `prompt`: `Square <album|single|EP|mixtape|playlist> cover art for "<title>" by <artist>, <genre> music.` then `Mood: <mood>.`, `Visual style: <style>.` (default: striking, original and atmospheric, one strong central image), the lettering line, and `Readable as a small thumbnail on streaming platforms, no frame, no mockup, no watermark.` Lettering: `Typography integrated into the artwork that reads exactly "<title>" and, smaller, "<artist>", no other text.` (default), the same with the title only, or `No text on the cover.`
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

Text only. Do not use this plugin for uploaded, attached or reference images or videos (editing, background removal, upscaling, image-to-video). For those, point the user to the Abracadabrax workspace at https://abracadabrax.app/workspace. Covers from text only. It does not put your own photo or band logo on the cover, edit an existing cover or make the music.
