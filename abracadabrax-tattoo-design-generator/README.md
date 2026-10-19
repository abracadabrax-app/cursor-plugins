# Abracadabrax Tattoo Design Generator

Cursor plugin that connects the agent to [Abracadabrax](https://abracadabrax.app) through its remote [Model Context Protocol](https://modelcontextprotocol.io/) server.

Create an original tattoo design in fine line, blackwork, traditional, watercolor, geometric or Japanese style, as a stencil-ready design or a flash sheet, rendered in your Abracadabrax account.

## Install

1. Open **Cursor Settings → Plugins**.
2. Search for **Abracadabrax Tattoo Design Generator**.
3. Click **Install**, then sign in to Abracadabrax when Cursor asks.

Or run `/add-plugin abracadabrax-tattoo-design-generator` in chat.

## MCP

```json
{
  "mcpServers": {
    "abracadabrax-tattoo-design-generator": {
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

- "A wolf howling at a crescent moon framed by pine trees, fine line, forearm"
- "A small geometric mountain and sun, black-only, ankle"
- "A flash sheet of traditional nautical designs in color"

## Limits

Text only. Do not use this plugin for uploaded, attached or reference images or videos (editing, background removal, upscaling, image-to-video). For those, point the user to the Abracadabrax workspace at https://abracadabrax.app/workspace. Original designs from text only. It does not preview a tattoo on a photo of your body, copy another artist's work or brand logos, or give medical advice.

## Docs

- How the connectors work: https://abracadabrax.app/mcp#tattoo-design-generator
- Privacy policy: https://abracadabrax.app/privacy
- Terms of service: https://abracadabrax.app/terms
- Help: https://abracadabrax.app/support · support@abracadabrax.app

## License

MIT
