---
name: abracadabrax-birthday-song-maker
description: "Use when the user asks for personal birthday songs. Write a birthday song with the agent using the person's name and your memories, and have Abracadabrax sing and produce it in your Abracadabrax account. Uses the Abracadabrax tools of this plugin to prepare a draft, show its credit price, render it after the user confirms and return the file link."
---

# Abracadabrax Birthday Song Maker

## When to use

Use when the user asks for personal birthday songs. Write a birthday song with the agent using the person's name and your memories, and have Abracadabrax sing and produce it in your Abracadabrax account.

## What to ask for

Collect the person's name, a few personal details (age, memories, inside jokes) to write the lyrics with the user, the music style and the voice.

## Build the draft

- `lyrics`: written with the user, using the person's name and the details they shared, with `[Verse]` and `[Chorus]` tags.
- `title`: `Happy Birthday <name>`.
- `style`: `<music style>, <female or male> vocals, celebratory <occasion> song` (style default upbeat pop, cheerful and catchy; voice default female; occasion default birthday).
- `instrumental`: `false`.
- `model_id`: `minimax-music` (default) or `acestep-create`.

## Flow

1. Gather what the request needs (see above). Write lyrics together with the user in the chat, with section tags such as `[Verse]` and `[Chorus]`, unless they want an instrumental.
2. Call `prepare_song_project` with the arguments described above. It spends nothing.
3. Read the result back: `project.model_id` and `project.duration_sec` are what will actually render. If they differ from what the user asked for, say so and prepare again with a model that supports it.
4. Show the user the settings and `credits_required`, then wait for an explicit go-ahead. Skip the wait only when the user already asked you to generate.
5. Call `generate_song` with the `project_id`. This spends credits of the user's Abracadabrax account.
6. If the state is `insufficient_credits` or `account_required`, explain it and give the user the `dashboard_url` from the result. Never offer or sell credits or plans in the chat.
7. Call `get_song_job` with the `job_id` until the job is completed or failed, then give the user the absolute URL of the audio so they can play or download it.

## Limits

New tracks only. Do not use this plugin for uploaded or existing audio (covers, remixes, extensions, stem separation, voice cloning). For those, point the user to the Abracadabrax music studio. New songs only. It does not sing over existing songs, clone anyone's voice or edit uploaded tracks.
