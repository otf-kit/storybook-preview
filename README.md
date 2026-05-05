# @otfdashkit/ui-native — Storybook Preview

Static phone-frame wrapper around the live `@otfdashkit/ui-native` storybook. Renders the storybook inside an iPhone-shaped SVG, with an Expo Go QR pairing card for native preview on a real device.

> **What this package is**: a single static `index.html` — no build step, no JS deps. Pure decoration for embedding the storybook on marketing surfaces.

## Run locally

```bash
npm run dev
# → http://localhost:4001
```

By default the iframe loads `https://native.otf-kit.dev`. Override the iframe source via query string:

```bash
open "http://localhost:4001?src=http://localhost:3010"
```

## Deploy to Cloudflare Pages

1. Sign up at [Cloudflare](https://dash.cloudflare.com) (free)
2. Get your Account ID (right sidebar of dashboard) and an API token (Profile → API Tokens → Create Token → "Edit Cloudflare Workers" template)
3. `cp .env.example .env` and fill both vars
4. `npm run deploy`

Live URL after first deploy: `https://otf-ui-native-storybook-preview.pages.dev` (or your own custom domain).

## How the phone frame works

The frame is a Manus-style two-bezel SVG (475×998 viewBox) with a `<foreignObject>` containing the iframe. The iframe sits at `y=78` so the dynamic island reads as iOS hardware over a black strip — content begins below it cleanly without needing safe-area padding inside the storybook itself.

## License

MIT
