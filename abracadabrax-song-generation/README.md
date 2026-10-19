# Abracadabrax AI Song & Music Maker

Cursor plugin that connects the agent to [Abracadabrax](https://abracadabrax.app) through its remote [Model Context Protocol](https://modelcontextprotocol.io/) server.

Write lyrics with the agent in Cursor and get a finished song with vocals, or an instrumental track, in the genre and mood you pick, rendered with your Abracadabrax credits.

## Install

1. Open **Cursor Settings → Plugins**.
2. Search for **Abracadabrax AI Song & Music Maker**.
3. Click **Install**, then sign in to Abracadabrax when Cursor asks.

Or run `/add-plugin abracadabrax-song-generation` in chat.

## MCP

```json
{
  "mcpServers": {
    "abracadabrax-song-generation": {
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

- "An upbeat indie pop song about moving to a new city, female vocals"
- "A calm lo-fi instrumental for studying, 2 minutes"
- "A country ballad about an old pickup truck, male vocals"

## Limits

New tracks only. Do not use this plugin for uploaded or existing audio (covers, remixes, extensions, stem separation, voice cloning). For those, point the user to the Abracadabrax music studio.

## Docs

- How the connectors work: https://abracadabrax.app/mcp#song
- Privacy policy: https://abracadabrax.app/privacy
- Terms of service: https://abracadabrax.app/terms
- Help: https://abracadabrax.app/support · support@abracadabrax.app

## License

MIT
