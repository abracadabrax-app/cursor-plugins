# Abracadabrax plugins for Cursor

Cursor plugins that let the agent create images, videos and songs with [Abracadabrax](https://abracadabrax.app). Each plugin connects to a hosted Abracadabrax MCP server and adds a skill for one kind of output. The agent prepares a draft, shows its price in credits, and renders only after you confirm.

| Plugin | What you get | Endpoint |
|---|---|---|
| [Abracadabrax AI Image & Video Generator](abracadabrax-video-image-generation) | Describe an image or a short video and get the file back in Cursor: pick the model, the aspect ratio and the length, check the credit price, then render it in your Abracadabrax account. | `/api/grok/media/mcp` |
| [Abracadabrax AI Image Generator](abracadabrax-image-generation) | Turn a text description into an image in Cursor: photos, illustrations, mockups and graphics with readable text, in the aspect ratio you need, rendered with your Abracadabrax credits. | `/api/grok/media/mcp` |
| [Abracadabrax AI Video Generator](abracadabrax-video-generation) | Turn a scene description into a short AI video clip in Cursor: landscape, vertical or square, 4 to 12 seconds, with Kling, Sora or Veo, rendered with your Abracadabrax credits. | `/api/grok/media/mcp` |
| [Abracadabrax AI Song & Music Maker](abracadabrax-song-generation) | Write lyrics with the agent in Cursor and get a finished song with vocals, or an instrumental track, in the genre and mood you pick, rendered with your Abracadabrax credits. | `/api/grok/song/mcp` |
| [Abracadabrax YouTube Thumbnail Maker](abracadabrax-youtube-thumbnail-maker) | Design a bold 16:9 video thumbnail from the topic of your video and a short headline, rendered in your Abracadabrax account. | `/api/grok/media/mcp` |
| [Abracadabrax AI Product Photo Generator](abracadabrax-product-photo-generator) | Turn a product description into a white-background packshot, a lifestyle scene, a flat lay, a hero banner or a close-up for a store or an ad, rendered in your Abracadabrax account. | `/api/grok/media/mcp` |
| [Abracadabrax Social Media Image & Post Maker](abracadabrax-social-media-image) | Turn a post idea into an image sized for Instagram, Facebook, LinkedIn, X, Pinterest or a vertical story, with optional text and brand colors, rendered in your Abracadabrax account. | `/api/grok/media/mcp` |
| [Abracadabrax Poster & Flyer Maker](abracadabrax-poster-flyer-maker) | Design a print-ready poster or flyer with the headline and the details of your event, sale or announcement laid out on it, rendered in your Abracadabrax account. | `/api/grok/media/mcp` |
| [Abracadabrax AI Background Music Generator](abracadabrax-background-music-generator) | Describe a mood and get an original instrumental track for a video, podcast, ad, game, stream or study session, produced in your Abracadabrax account. | `/api/grok/song/mcp` |
| [Abracadabrax Birthday Song Maker](abracadabrax-birthday-song-maker) | Write a birthday song with the agent using the person's name and your memories, and have Abracadabrax sing and produce it in your Abracadabrax account. | `/api/grok/song/mcp` |
| [Abracadabrax Album Cover Art Maker](abracadabrax-album-cover-maker) | Design square cover art for an album, single, EP, mixtape or playlist from the title, the artist, the genre and the mood, rendered in your Abracadabrax account. | `/api/grok/media/mcp` |
| [Abracadabrax Coloring Page Maker](abracadabrax-coloring-page-maker) | Draw a printable black-and-white coloring page from a subject or a scene, simple for toddlers, detailed for kids or intricate for adults, rendered in your Abracadabrax account. | `/api/grok/media/mcp` |
| [Abracadabrax Greeting Card & Invitation Maker](abracadabrax-greeting-card-maker) | Design a personal greeting card or invitation for a birthday, wedding, anniversary, baby shower, holiday or thank-you, with your message printed on it, rendered in your Abracadabrax account. | `/api/grok/media/mcp` |
| [Abracadabrax Podcast Intro & Jingle Maker](abracadabrax-podcast-jingle-maker) | Produce a 30 or 60 second intro or outro jingle for a podcast, channel or stream, instrumental or with a sung tagline that says the show's name, in your Abracadabrax account. | `/api/grok/song/mcp` |
| [Abracadabrax AI Character Generator](abracadabrax-ai-character-generator) | Design an original character for a fantasy or RPG campaign, a video game, a story or a mascot, as a portrait, a full-body figure or a character sheet, rendered in your Abracadabrax account. | `/api/grok/media/mcp` |
| [Abracadabrax Sticker & Emoji Maker](abracadabrax-sticker-emoji-maker) | Create a custom die-cut sticker or emoji-style icon, one design or a set of 4, 6 or 9, with optional short text, on a plain background ready to cut out, rendered in your Abracadabrax account. | `/api/grok/media/mcp` |
| [Abracadabrax Tattoo Design Generator](abracadabrax-tattoo-design-generator) | Create an original tattoo design in fine line, blackwork, traditional, watercolor, geometric or Japanese style, as a stencil-ready design or a flash sheet, rendered in your Abracadabrax account. | `/api/grok/media/mcp` |
| [Abracadabrax Fantasy Map Generator](abracadabrax-fantasy-map-generator) | Create a map of an imaginary world, continent, kingdom, island, city or dungeon for your tabletop campaign, novel or game, with the place names you choose, rendered in your Abracadabrax account. | `/api/grok/media/mcp` |
| [Abracadabrax AI Wallpaper Maker](abracadabrax-ai-wallpaper-maker) | Create a wallpaper from a theme and a style, sized for phone, desktop, tablet or a square screen with space kept clear for icons and the clock, rendered in your Abracadabrax account. | `/api/grok/media/mcp` |
| [Abracadabrax Pixel Art & Game Sprite Generator](abracadabrax-pixel-art-generator) | Create 8-bit or 16-bit pixel art for indie games and posts: a character sprite, a sprite sheet, items and icons, a tileset or a full scene, rendered in your Abracadabrax account. | `/api/grok/media/mcp` |
| [Abracadabrax T-Shirt Design Maker](abracadabrax-tshirt-design-maker) | Create an original graphic and optional slogan for t-shirts, hoodies and print-on-demand merch, centered on a plain background in the color of the garment, rendered in your Abracadabrax account. | `/api/grok/media/mcp` |
| [Abracadabrax Comic Strip Maker](abracadabrax-comic-strip-maker) | Create an original comic strip of 3, 4 or 6 panels with speech bubbles from your story and characters, in cartoon, manga, newspaper or graphic novel style, rendered in your Abracadabrax account. | `/api/grok/media/mcp` |
| [Abracadabrax Book Cover Maker](abracadabrax-book-cover-maker) | Create a front cover for an ebook, a Kindle book or a print book in 2:3 portrait format, with the title, the subtitle and the author name set in the design, rendered in your Abracadabrax account. | `/api/grok/media/mcp` |
| [Abracadabrax App Icon Generator](abracadabrax-app-icon-generator) | Create an app icon for iOS, Android, web or desktop apps: one bold symbol on a rounded square, in the style and colors of your app, rendered in your Abracadabrax account. | `/api/grok/media/mcp` |

All endpoints are on `https://abracadabrax.app`.

## Install

Open **Cursor Settings → Plugins**, search for **Abracadabrax** and install the plugin you want, or run `/add-plugin <name>` in chat.

## Auth

Cursor asks you to sign in to Abracadabrax when the plugin connects (OAuth 2.1 with PKCE). You can create an account on the same page.

## Pricing

The plugin is free. Renders use credits of your Abracadabrax account: a new account starts with a $1, 3-day trial that includes 140 credits, then Solo is $34/month (3,000 credits), Studio $47/month (9,300 credits) or Atelier $117/month (27,000 credits). Every draft shows its price in credits before anything is rendered, and nothing is charged until you confirm.

All images, videos and songs are produced by generative AI models, and only when you confirm.

## Links

- [How the connectors work](https://abracadabrax.app/mcp)
- [Privacy policy](https://abracadabrax.app/privacy) · [Terms of service](https://abracadabrax.app/terms)
- [Help](https://abracadabrax.app/support) · support@abracadabrax.app

## License

Released under the MIT license, see [LICENSE](LICENSE). Cursor is a product of Anysphere; Abracadabrax is a separate product and this repository is not a Cursor project.
