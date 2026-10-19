---
name: abracadabrax-greeting-card-maker
description: "Use when the user asks for personal cards and invitations. Design a personal greeting card or invitation for a birthday, wedding, anniversary, baby shower, holiday or thank-you, with your message printed on it, rendered in your Abracadabrax account. Uses the Abracadabrax tools of this plugin to prepare a draft, show its credit price, render it after the user confirms and return the file link."
---

# Abracadabrax Greeting Card & Invitation Maker

## When to use

Use when the user asks for personal cards and invitations. Design a personal greeting card or invitation for a birthday, wedding, anniversary, baby shower, holiday or thank-you, with your message printed on it, rendered in your Abracadabrax account.

## What to ask for

Collect the occasion, whether it is a greeting card or an invitation, who it is for, the message to print, the event details for an invitation and the card style.

## Build the draft

- `tab`: `image`.
- `prompt`: `Front of a personal <occasion> <greeting card|invitation> for <recipient>.` `Main text, spelled exactly: "<message>".` (up to about 160 characters), for invitations `Smaller text, spelled exactly: "<date, time, place, RSVP>".`, then `Style: <style>.` (default: warm, heartfelt and elegant, with a decorative illustration framing the text) and `Flat card design filling the whole image, print-ready, no other text, no mockup, no watermark.` Occasions: birthday, wedding, anniversary, baby shower, holiday season, thank-you, graduation, get well soon, congratulations, party.
- `ratio`: `3:4` portrait (default), `4:3` landscape or `1:1`.
- `model_id`: `nano-banana-pro` (default, sharp text), `gpt-image-2`, `nano-banana-2`.

## Flow

1. Gather what the request needs (see above). Ask only for what is missing; sensible defaults are fine.
2. Call `prepare_media_project` with the arguments described above. It spends nothing.
3. Read the result back. `project.model_id`, `project.ratio` and `project.duration` are what will actually render: the server replaces an unknown model id with its default model, and a ratio or a length the model does not support with the model's default. If any of them differs from what the user asked for, say so and prepare again with a model that supports it.
4. Show the user the settings and `credits_required`, then wait for an explicit go-ahead. Skip the wait only when the user already asked you to generate.
5. Call `generate_media` with the `project_id`. This spends credits of the user's Abracadabrax account.
6. If the state is `insufficient_credits` or `account_required`, explain it and give the user the `dashboard_url` from the result. Never offer or sell credits or plans in the chat.
7. Call `get_media_job` with the `job_id` until the job is completed or failed, then give the user the absolute URL of the file so they can open or download it.

## Limits

Text only. Do not use this plugin for uploaded, attached or reference images or videos (editing, background removal, upscaling, image-to-video). For those, point the user to the Abracadabrax workspace at https://abracadabrax.app/workspace. Cards from text only. It does not add your own photos, print or mail the card, or design posters for public events.
