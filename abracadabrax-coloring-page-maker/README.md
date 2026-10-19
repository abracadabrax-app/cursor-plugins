# Abracadabrax Coloring Page Maker

Cursor plugin that connects the agent to [Abracadabrax](https://abracadabrax.app) through its remote [Model Context Protocol](https://modelcontextprotocol.io/) server.

Draw a printable black-and-white coloring page from a subject or a scene, simple for toddlers, detailed for kids or intricate for adults, rendered in your Abracadabrax account.

## Install

1. Open **Cursor Settings → Plugins**.
2. Search for **Abracadabrax Coloring Page Maker**.
3. Click **Install**, then sign in to Abracadabrax when Cursor asks.

Or run `/add-plugin abracadabrax-coloring-page-maker` in chat.

## MCP

```json
{
  "mcpServers": {
    "abracadabrax-coloring-page-maker": {
      "type": "http",
      "url": "https://abracadabrax.app/api/grok/media/mcp"
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
| `prepare_media_project` | Saves a draft (image or video, prompt, model, aspect ratio, length) and returns the credits it will cost | none |
| `generate_media` | Starts the render of a prepared draft, only after you confirm | charged |
| `get_media_job` | Reports progress and returns the link to the finished file | none |

The skill in this plugin tells the agent how to write the draft for this kind of output and to wait for your confirmation before rendering.

## Try asking

- "A coloring page of a dinosaur playing football for my 4-year-old"
- "An intricate mandala with flowers for adult coloring, square page"
- "A castle with dragons and a moat, with a background scene to color, for a 7-year-old"

## Limits

Text only. Do not use this plugin for uploaded, attached or reference images or videos (editing, background removal, upscaling, image-to-video). For those, point the user to the Abracadabrax workspace at https://abracadabrax.app/workspace. Pages from text only. It does not turn your own photo or drawing into a coloring page or color it in.

## Docs

- How the connectors work: https://abracadabrax.app/mcp#coloring-page-maker
- Privacy policy: https://abracadabrax.app/privacy
- Terms of service: https://abracadabrax.app/terms
- Help: https://abracadabrax.app/support · support@abracadabrax.app

## License

MIT
