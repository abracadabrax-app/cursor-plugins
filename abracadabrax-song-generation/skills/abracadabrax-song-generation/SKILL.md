---
name: abracadabrax-song-generation
description: "The user wants a new song with vocals or a new instrumental track created from a description and lyrics. Uses the Abracadabrax tools of this plugin to prepare a draft, show its credit price, render it after the user confirms and return the file link."
---

# Abracadabrax AI Song & Music Maker

## When to use

The user wants a new song with vocals or a new instrumental track created from a description and lyrics.

## What to ask for

Collect the genre, mood, tempo and voice, the lyrics (written together in the chat) or whether it is an instrumental, an optional title and the length.

## Build the draft

- `style` (required): genre, mood, tempo, instruments and vocal style, up to 600 characters, for example `upbeat indie pop, female vocals, 120 bpm, bright guitars`.
- `lyrics`: the full lyrics with section tags, up to 3,000 characters. Omit for an instrumental.
- `instrumental`: `true` for a track without vocals.
- `title` (optional), up to 120 characters.
- `duration_sec` (optional) and `model_id` (optional): see the note below.

**Models and lengths.** `minimax-music` (default) sings your lyrics but ignores `duration_sec`. Only `stable-audio` (instrumental), `acestep-create` (lyrics, chosen length) and `elevenlabs-music` (studio quality, no lyrics, more credits) honor `duration_sec`, with 30, 60, 120 or 180 seconds (300 also on `stable-audio` and `elevenlabs-music`). Lyrics on a model that cannot sing them switch the draft to a lyrics model, and a length the model does not support becomes its default.

## Flow

1. Gather what the request needs (see above). Write lyrics together with the user in the chat, with section tags such as `[Verse]` and `[Chorus]`, unless they want an instrumental.
2. Call `prepare_song_project` with the arguments described above. It spends nothing.
3. Read the result back: `project.model_id` and `project.duration_sec` are what will actually render. If they differ from what the user asked for, say so and prepare again with a model that supports it.
4. Show the user the settings and `credits_required`, then wait for an explicit go-ahead. Skip the wait only when the user already asked you to generate.
5. Call `generate_song` with the `project_id`. This spends credits of the user's Abracadabrax account.
6. If the state is `insufficient_credits` or `account_required`, explain it and give the user the `dashboard_url` from the result. Never offer or sell credits or plans in the chat.
7. Call `get_song_job` with the `job_id` until the job is completed or failed, then give the user the absolute URL of the audio so they can play or download it.

## Limits

New tracks only. Do not use this plugin for uploaded or existing audio (covers, remixes, extensions, stem separation, voice cloning). For those, point the user to the Abracadabrax music studio.
