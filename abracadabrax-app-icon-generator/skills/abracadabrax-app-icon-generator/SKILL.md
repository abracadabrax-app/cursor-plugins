---
name: abracadabrax-app-icon-generator
description: "Use when the user asks for icons for iOS, Android and web. Create an app icon for iOS, Android, web or desktop apps: one bold symbol on a rounded square, in the style and colors of your app, rendered in your Abracadabrax account. Uses the Abracadabrax tools of this plugin to prepare a draft, show its credit price, render it after the user confirms and return the file link."
---

# Abracadabrax App Icon Generator

## When to use

Use when the user asks for icons for iOS, Android and web. Create an app icon for iOS, Android, web or desktop apps: one bold symbol on a rounded square, in the style and colors of your app, rendered in your Abracadabrax account.

## What to ask for

Collect what the app does, any symbol idea, the icon style and the brand colors.

## Build the draft

- `tab`: `image`.
- `ratio`: `1:1`.
- `prompt`: `App icon for <what the app does>.` then `Symbol: <symbol>.` or `One simple, memorable symbol that says what the app does.`, the style line, `Colors: <colors>.` when given, and `Rounded square icon filling the image, centered, readable at small sizes, original design, no text, no letters, no existing brand logos, no watermark.`
  - style: `Style: flat design with solid colors.` (default), `Style: vibrant gradient background with a clean white symbol.`, `Style: soft glossy 3D symbol with subtle depth.` or `Style: minimal line symbol on a solid color.`
- `model_id`: `nano-banana-2` (default), `nano-banana-pro`, `gpt-image-2`.

## Flow

1. Gather what the request needs (see above). Ask only for what is missing; sensible defaults are fine.
2. Call `prepare_media_project` with the arguments described above. It spends nothing.
3. Read the result back. `project.model_id`, `project.ratio` and `project.duration` are what will actually render: the server replaces an unknown model id with its default model, and a ratio or a length the model does not support with the model's default. If any of them differs from what the user asked for, say so and prepare again with a model that supports it.
4. Show the user the settings and `credits_required`, then wait for an explicit go-ahead. Skip the wait only when the user already asked you to generate.
5. Call `generate_media` with the `project_id`. This spends credits of the user's Abracadabrax account.
6. If the state is `insufficient_credits` or `account_required`, explain it and give the user the `dashboard_url` from the result. Never offer or sell credits or plans in the chat.
7. Call `get_media_job` with the `job_id` until the job is completed or failed, then give the user the absolute URL of the file so they can open or download it.

## Limits

Text only. Do not use this plugin for uploaded, attached or reference images or videos (editing, background removal, upscaling, image-to-video). For those, point the user to the Abracadabrax workspace at https://abracadabrax.app/workspace. New icons from text only. It does not redraw an existing logo or brand, export icon size sets or vector files, or check trademarks.
Original designs only. Do not use it for copyrighted characters, existing franchises, brand logos, trademarks or real celebrities; offer the user an original alternative instead.
