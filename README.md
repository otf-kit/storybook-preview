# @otf/ui-native — Storybook Preview

Standalone marketing/preview shell for [`apps/ui-native-storybook`](../ui-native-storybook). Same recipe as [`kits/fitness-kit-preview`](../../kits/fitness-kit-preview) — the canonical kit-preview pattern.

A single static `index.html` that:

- Renders the storybook's live web URL inside an iPhone-shaped SVG mockup
- Pairs it with an Expo Go QR card so visitors can run the live storybook on their phone
- Falls back to a floating QR-modal trigger on viewports < 900px

## Run locally

```bash
cd apps/ui-native-storybook-preview
npm run dev
# → http://localhost:4001
```

By default the iframe loads `https://otf-ui-native-storybook.pages.dev`. To point at a local storybook dev server:

```bash
# Terminal 1: actual storybook
cd ../ui-native-storybook && npm run dev

# Terminal 2: preview frame, override iframe src via query
open "http://localhost:4001?src=http://localhost:3010"
```

## Deploy

Cloudflare Pages, project `otf-ui-native-storybook-preview`. Reads credentials from repo-root `.env` (`CLOUDFLARE_ACCOUNT_ID` + `CLOUDFLARE_API_TOKEN`).

```bash
cd apps/ui-native-storybook-preview
npm run deploy
# → https://otf-ui-native-storybook-preview.pages.dev
```

First-time setup:

```bash
set -a && . ../../.env && set +a
npx wrangler pages project create otf-ui-native-storybook-preview --production-branch main
npm run deploy
```

## Why a separate package

The storybook is the product (the actual responsive component browser at `otf-ui-native-storybook.pages.dev`). This package is **decoration** — wraps the storybook URL in a phone frame for the marketing landing page. Same reasoning as `kits/fitness-kit-preview/`:
- Excluded from pnpm workspace via `!apps/ui-native-storybook-preview` (avoids React #527 dual-instance crashes)
- Pure static HTML — no JS deps, no build step

## Recipe — see fitness-kit-preview

All design recipes (Manus-style SVG geometry, landing-matched grid bg, iframe full-bleed rule, QR card centering) are documented in [`kits/fitness-kit-preview/README.md`](../../kits/fitness-kit-preview/README.md). This package is a near-identical copy with two changes:
1. `DEFAULT_KIT_URL` → `https://otf-ui-native-storybook.pages.dev`
2. Title + description text

Don't drift from that recipe — copy fixes both ways.

## Dynamic island clearance — iframe at SVG y=78 (no kit-side shim)

This preview uses the same approach as `apps/landing/components/otf/ComponentDetail.tsx`'s `MobilePreview`: the foreignObject is at `y="78" height="906"` instead of `y="13.67" height="970"`. The iframe physically starts BELOW the dynamic island, and the 64px strip above it shows the SVG rect's `fill="black"` — pure black, where iOS' status bar would sit.

This means the storybook itself needs **no** `WebSafeAreaShim` — content sits at the top of the iframe naturally. Cleaner than fitness-kit's full-bleed-iframe approach (which requires the kit to add safe-area padding to clear the island).

Different from `kits/fitness-kit-preview/` which uses `y="13.67"` with a kit-side `WebSafeAreaShim` because fitness's welcome screen has a full-bleed hero image that's meant to extend under the dynamic island. See the kit-preview memory note for the decision rule.
