# Abracadabrax Podcast Intro & Jingle Maker

Cursor plugin that connects the agent to [Abracadabrax](https://abracadabrax.app) through its remote [Model Context Protocol](https://modelcontextprotocol.io/) server.

Produce a 30 or 60 second intro or outro jingle for a podcast, channel or stream, instrumental or with a sung tagline that says the show's name, in your Abracadabrax account.

## Install

1. Open **Cursor Settings → Plugins**.
2. Search for **Abracadabrax Podcast Intro & Jingle Maker**.
3. Click **Install**, then sign in to Abracadabrax when Cursor asks.

Or run `/add-plugin abracadabrax-podcast-jingle-maker` in chat.

## MCP

```json
{
  "mcpServers": {
    "abracadabrax-podcast-jingle-maker": {
      "type": "http",
      "url": "https://abracadabrax.app/api/grok/song/mcp"
    }
  }
}
```

## Auth

Cursor asks you to sign in to Abracadabrax when the plugin connects (OAuth 2.1 with PKCE). You can create an account on the same page.

## Pricing

The plugin is free. Renders use credits of your Abracadabrax account: a new account starts with a $1, 3-day trial that includes 140 credits, then Solo is $34/month (3,000 credits), Studio $47/month (9,300 credits) or Atelier $117/month (27,000 credits). Every draft shows its price in credits before anything is rendered, and nothing is charged until you confirm.

## Tools

| Tool | What it does | Credits |
|---|---|---|
| `prepare_song_project` | Saves a draft (title, style, lyrics or instrumental, length, model) and returns the credits it will cost | none |
| `generate_song` | Starts the render of a prepared draft, only after you confirm | charged |
| `get_song_job` | Reports progress and returns the link to the finished audio | none |

The skill in this plugin tells the agent how to write the draft for this kind of output and to wait for your confirmation before rendering.

## Try asking

- "A 30-second intro jingle for my podcast "The Morning Brew", upbeat and friendly, funky bass"
- "A sung tagline "You're listening to Deep Dive" with a female voice, synth pop, 60 seconds"
- "An instrumental outro for a cozy book review channel called Shelf Life"

## Limits

New tracks only. Do not use this plugin for uploaded or existing audio (covers, remixes, extensions, stem separation, voice cloning). For those, point the user to the Abracadabrax music studio. Short new tracks from text only. It does not make full-length songs, remix or extend existing recordings, or clone voices.

## Docs

- How the connectors work: https://abracadabrax.app/mcp#podcast-jingle-maker
- Privacy policy: https://abracadabrax.app/privacy
- Terms of service: https://abracadabrax.app/terms
- Help: https://abracadabrax.app/support · support@abracadabrax.app

## License

MIT
