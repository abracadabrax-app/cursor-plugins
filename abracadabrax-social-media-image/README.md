# Abracadabrax Social Media Image & Post Maker

Cursor plugin that connects the agent to [Abracadabrax](https://abracadabrax.app) through its remote [Model Context Protocol](https://modelcontextprotocol.io/) server.

Turn a post idea into an image sized for Instagram, Facebook, LinkedIn, X, Pinterest or a vertical story, with optional text and brand colors, rendered in your Abracadabrax account.

## Install

1. Open **Cursor Settings → Plugins**.
2. Search for **Abracadabrax Social Media Image & Post Maker**.
3. Click **Install**, then sign in to Abracadabrax when Cursor asks.

Or run `/add-plugin abracadabrax-social-media-image` in chat.

## MCP

```json
{
  "mcpServers": {
    "abracadabrax-social-media-image": {
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

- "Instagram post announcing our autumn menu, warm tones, text "Now serving""
- "Pinterest pin of a cozy reading nook, text "Cozy season""
- "LinkedIn post image about remote team rituals, clean flat illustration"

## Limits

Text only. Do not use this plugin for uploaded, attached or reference images or videos (editing, background removal, upscaling, image-to-video). For those, point the user to the Abracadabrax workspace at https://abracadabrax.app/workspace. New images only. It does not edit photos you already have, add your logo file, or publish or schedule posts.

## Docs

- How the connectors work: https://abracadabrax.app/mcp#social-media-image
- Privacy policy: https://abracadabrax.app/privacy
- Terms of service: https://abracadabrax.app/terms
- Help: https://abracadabrax.app/support · support@abracadabrax.app

## License

MIT
