---
name: abracadabrax-tattoo-design-generator
description: "Use when the user asks for original tattoo designs. Create an original tattoo design in fine line, blackwork, traditional, watercolor, geometric or Japanese style, as a stencil-ready design or a flash sheet, rendered in your Abracadabrax account. Uses the Abracadabrax tools of this plugin to prepare a draft, show its credit price, render it after the user confirms and return the file link."
---

# Abracadabrax Tattoo Design Generator

## When to use

Use when the user asks for original tattoo designs. Create an original tattoo design in fine line, blackwork, traditional, watercolor, geometric or Japanese style, as a stencil-ready design or a flash sheet, rendered in your Abracadabrax account.

## What to ask for

Collect the tattoo idea, the style, black-and-gray, black-only or color ink, the body placement and whether it is one stencil design or a flash sheet.

## Build the draft

- `tab`: `image`.
- `ratio`: `3:4`.
- `prompt`: `Original tattoo design: <idea>.` `Tattoo style: <style>.` (default fine line), the ink line, `Shaped to fit the <placement>.` when given, the layout line and `Shown as a design drawing, not on skin, no text, no watermark.`
  - ink: `Black ink only with gray shading.` (default), `Pure black ink line work, no shading.` or `Full color ink.`
  - layout: `One tattoo design, clean and stencil-ready, centered on a plain white background like a tattoo flash drawing.` (default) or `A tattoo flash sheet with several small matching designs arranged on a plain white background.`
- `model_id`: `nano-banana-pro` (default), `flux-2-pro`, `nano-banana-2`.

## Flow

1. Gather what the request needs (see above). Ask only for what is missing; sensible defaults are fine.
2. Call `prepare_media_project` with the arguments described above. It spends nothing.
3. Read the result back. `project.model_id`, `project.ratio` and `project.duration` are what will actually render: the server replaces an unknown model id with its default model, and a ratio or a length the model does not support with the model's default. If any of them differs from what the user asked for, say so and prepare again with a model that supports it.
4. Show the user the settings and `credits_required`, then wait for an explicit go-ahead. Skip the wait only when the user already asked you to generate.
5. Call `generate_media` with the `project_id`. This spends credits of the user's Abracadabrax account.
6. If the state is `insufficient_credits` or `account_required`, explain it and give the user the `dashboard_url` from the result. Never offer or sell credits or plans in the chat.
7. Call `get_media_job` with the `job_id` until the job is completed or failed, then give the user the absolute URL of the file so they can open or download it.

## Limits

Text only. Do not use this plugin for uploaded, attached or reference images or videos (editing, background removal, upscaling, image-to-video). For those, point the user to the Abracadabrax workspace at https://abracadabrax.app/workspace. Original designs from text only. It does not preview a tattoo on a photo of your body, copy another artist's work or brand logos, or give medical advice.
Original designs only. Do not use it for copyrighted characters, existing franchises, brand logos, trademarks or real celebrities; offer the user an original alternative instead.
