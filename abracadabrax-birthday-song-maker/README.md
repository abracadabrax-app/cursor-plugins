# Abracadabrax Birthday Song Maker

Cursor plugin that connects the agent to [Abracadabrax](https://abracadabrax.app) through its remote [Model Context Protocol](https://modelcontextprotocol.io/) server.

Write a birthday song with the agent using the person's name and your memories, and have Abracadabrax sing and produce it in your Abracadabrax account.

## Install

1. Open **Cursor Settings → Plugins**.
2. Search for **Abracadabrax Birthday Song Maker**.
3. Click **Install**, then sign in to Abracadabrax when Cursor asks.

Or run `/add-plugin abracadabrax-birthday-song-maker` in chat.

## MCP

```json
{
  "mcpServers": {
    "abracadabrax-birthday-song-maker": {
      "type": "http",
      "url": "https://abracadabrax.app/api/grok/song/mcp"
    }
  }
}
```

## Auth

Cursor asks you to sign in to Abracadabrax when the plugin connects (OAuth 2.1 with PKCE). You can create an account on the same page.

## Pricing

The plugin is free. Renders use credits of your Abracadabrax account: a new account starts with a $1, 7-day trial that includes 140 credits, then Solo is $34/month (3,000 credits), Studio $47/month (9,300 credits) or Atelier $117/month (27,000 credits). Every draft shows its price in credits before anything is rendered, and nothing is charged until you confirm.

## Tools

| Tool | What it does | Credits |
|---|---|---|
| `prepare_song_project` | Saves a draft (title, style, lyrics or instrumental, length, model) and returns the credits it will cost | none |
| `generate_song` | Starts the render of a prepared draft, only after you confirm | charged |
| `get_song_job` | Reports progress and returns the link to the finished audio | none |

The skill in this plugin tells the agent how to write the draft for this kind of output and to wait for your confirmation before rendering.

## Try asking

- "A happy birthday song for my sister Giulia, she turns 30 and loves surfing"
- "An acoustic birthday song for my dad, with a line about his terrible jokes"
- "A funny pop-punk birthday song for my best friend Sam"

## Limits

New tracks only. Do not use this plugin for uploaded or existing audio (covers, remixes, extensions, stem separation, voice cloning). For those, point the user to the Abracadabrax music studio. New songs only. It does not sing over existing songs, clone anyone's voice or edit uploaded tracks.

## Docs

- How the connectors work: https://abracadabrax.app/mcp#birthday-song-maker
- Privacy policy: https://abracadabrax.app/privacy
- Terms of service: https://abracadabrax.app/terms
- Help: https://abracadabrax.app/support · support@abracadabrax.app

## License

MIT
