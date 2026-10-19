---
name: abracadabrax-video-generation
description: "The user wants a new short video clip created from a text description: a scene, a product shot, a social clip, a b-roll shot. Uses the Abracadabrax tools of this plugin to prepare a draft, show its credit price, render it after the user confirms and return the file link."
---

# Abracadabrax AI Video Generator

## When to use

The user wants a new short video clip created from a text description: a scene, a product shot, a social clip, a b-roll shot.

## What to ask for

Collect what happens in the clip (subject, action, setting, camera movement, lighting), the visual style, the format (landscape, vertical or square) and the length.

## Build the draft

- `tab`: always `video`.
- `prompt`: the scene, up to 3,000 characters, with the visual style on its own line (for example `Visual style: cinematic.`).
- `ratio`: `16:9` landscape (default), `9:16` vertical, or `1:1` square on Kling only.
- `duration`: seconds, one of the lengths the chosen model supports.
- `model_id` (optional): `kling-3-pro` (default), `sora-2`, `veo-3-1`.

**Video formats and lengths.** `kling-3-pro` (default) takes `16:9`, `9:16` or `1:1` and 5 or 10 seconds. `sora-2` takes `16:9` or `9:16` and 4, 8 or 12 seconds. `veo-3-1` takes `16:9` or `9:16` and 4, 6 or 8 seconds. A format or a length the model does not support is silently replaced with the model's default.

## Flow

1. Gather what the request needs (see above). Ask only for what is missing; sensible defaults are fine.
2. Call `prepare_media_project` with `tab` set to `video`, `prompt`, `ratio`, `duration` and, when needed, `model_id`. It spends nothing.
3. Read the result back. `project.model_id`, `project.ratio` and `project.duration` are what will actually render: the server replaces an unknown model id with its default model, and a ratio or a length the model does not support with the model's default. If any of them differs from what the user asked for, say so and prepare again with a model that supports it.
4. Show the user the settings and `credits_required`, then wait for an explicit go-ahead. Skip the wait only when the user already asked you to generate.
5. Call `generate_media` with the `project_id`. This spends credits of the user's Abracadabrax account.
6. If the state is `insufficient_credits` or `account_required`, explain it and give the user the `dashboard_url` from the result. Never offer or sell credits or plans in the chat.
7. Call `get_media_job` with the `job_id` until the job is completed or failed, then give the user the absolute URL of the file so they can open or download it.

## Limits

Text only. Do not use this plugin for uploaded, attached or reference images or videos (editing, background removal, upscaling, image-to-video). For those, point the user to the Abracadabrax workspace at https://abracadabrax.app/workspace. It does not animate photos, edit or extend existing videos, or add lip sync.
