---
name: abracadabrax-podcast-jingle-maker
description: "Use when the user asks for intros that say your show. Produce a 30 or 60 second intro or outro jingle for a podcast, channel or stream, instrumental or with a sung tagline that says the show's name, in your Abracadabrax account. Uses the Abracadabrax tools of this plugin to prepare a draft, show its credit price, render it after the user confirms and return the file link."
---

# Abracadabrax Podcast Intro & Jingle Maker

## When to use

Use when the user asks for intros that say your show. Produce a 30 or 60 second intro or outro jingle for a podcast, channel or stream, instrumental or with a sung tagline that says the show's name, in your Abracadabrax account.

## What to ask for

Collect the show's name, its mood and genre, whether the jingle is instrumental or sings a short tagline with the show's name, and the length (30 or 60 seconds).

## Build the draft

- `title`: `<show> Intro`.
- `style`: `<genre> intro jingle for the show "<show>", <mood>, short, catchy signature theme with a clear start and a clean ending,` then `no vocals` or `<female|male> vocals singing a short tagline` (genre default upbeat modern).
- Instrumental (default): `instrumental: true`, no lyrics, `model_id` `stable-audio` (default) or `acestep-create`.
- Sung tagline: `instrumental: false`, `lyrics` `[Chorus]` followed by the tagline (default: the show's name), and `model_id` must be `acestep-create`.
- `duration_sec`: 30 (default) or 60. Only `stable-audio` and `acestep-create` keep a jingle this short; any other model returns a full-length song.

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

New tracks only. Do not use this plugin for uploaded or existing audio (covers, remixes, extensions, stem separation, voice cloning). For those, point the user to the Abracadabrax music studio. Short new tracks from text only. It does not make full-length songs, remix or extend existing recordings, or clone voices.
