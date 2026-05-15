<h1 align="center">@otfdashkit / storybook-preview</h1>

<p align="center">
  Static phone-frame wrapper around the live <code>@otfdashkit/ui-native</code> storybook.<br/>
  Pure HTML &mdash; one file, no build step, deploys to Cloudflare Pages.
</p>

<p align="center">
  <a href="https://native-preview.otf-kit.dev/" target="_blank">
    <img src="https://img.shields.io/badge/live-native--preview.otf--kit.dev-000?style=flat-square" alt="live">
  </a>
  <img src="https://img.shields.io/badge/License-MIT-blue.svg?style=flat-square" alt="MIT License">
  <img src="https://img.shields.io/badge/zero%20deps-yes-000?style=flat-square" alt="zero deps">
  <img src="https://img.shields.io/badge/host-Cloudflare%20Pages-000?style=flat-square" alt="Cloudflare Pages">
</p>

---

## Preview

<p align="center">
  <a href="https://native-preview.otf-kit.dev/" target="_blank">
    <img src="https://api.microlink.io/?url=https%3A%2F%2Fnative-preview.otf-kit.dev%2F&screenshot=true&meta=false&embed=screenshot.url&waitForTimeout=3000" alt="Storybook preview shell" width="100%" />
  </a>
</p>

<p align="center">
  <b><a href="https://native-preview.otf-kit.dev/">native-preview.otf-kit.dev</a></b><br/>
  <sub>Two-bezel iPhone-shaped SVG wrapping the live native storybook iframe, with an Expo Go QR pairing card for real-device preview.</sub>
</p>

> [!NOTE]
> This package is **a single static `index.html`** &mdash; no build step, no JS dependencies. Pure decoration for embedding the storybook on marketing surfaces.

## Run locally

```bash
npm run dev
# → http://localhost:4001
```

By default the iframe loads `https://native.otf-kit.dev`. Override via query string:

```bash
open "http://localhost:4001?src=http://localhost:3010"
```

## Deploy to Cloudflare Pages

1. Sign up at [Cloudflare](https://dash.cloudflare.com) (free tier is enough)
2. Get your **Account ID** (right sidebar of dashboard) and an **API token** (Profile → API Tokens → Create Token → "Edit Cloudflare Workers" template)
3. `cp .env.example .env` and fill both vars
4. `npm run deploy`

First deploy lands at `https://otf-ui-native-storybook-preview.pages.dev` &mdash; then point the `native-preview.otf-kit.dev` custom domain at it from the Pages dashboard. The bare showcase lives at `native.otf-kit.dev` (project `otf-ui-native-storybook`); the iframe in this shell loads that URL.

## How the phone frame works

The frame is a Manus-style two-bezel SVG (`475×998` viewBox) with a `<foreignObject>` containing the iframe. The iframe sits at `y=78` so the dynamic island reads as iOS hardware over a black strip &mdash; content begins below it cleanly without needing safe-area padding inside the storybook itself.

> [!TIP]
> To re-skin the frame, edit the SVG `<rect>` fills inside `index.html`. Everything else &mdash; layout, QR card, iframe geometry &mdash; cascades from the same file.

## Related

- [`@otfdashkit/sdk`](https://github.com/otf-kit/sdk) &mdash; the SDK whose native storybook this frame wraps
- [`saas-dashboard`](https://github.com/otf-kit/saas-dashboard) &mdash; web reference app
- [`fitness-kit`](https://github.com/otf-kit/fitness-kit) &mdash; mobile reference app

## License

MIT

---

Project home: [otf-kit.dev](https://otf-kit.dev) — the full OTF catalog.
