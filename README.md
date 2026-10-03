# OTF Native Preview

**A static phone frame around the live OTF UI Native component gallery, with an Expo Go QR card.**

[Live preview](https://native-preview.otf-kit.dev/) · [Full gallery](https://native.otf-kit.dev/) · [Native package](https://www.npmjs.com/package/@otfdashkit/ui-native)

[![Screenshot of the OTF native preview](https://api.microlink.io/?url=https%3A%2F%2Fnative-preview.otf-kit.dev%2F&screenshot=true&meta=false&embed=screenshot.url&waitForTimeout=3000)](https://native-preview.otf-kit.dev/)

## Run locally

```bash
npm install
npm run dev
```

Open `http://localhost:4001`. The frame loads `https://native.otf-kit.dev/` by default. To point it at a local gallery, open `http://localhost:4001?src=http://localhost:3010`.

## How it works

`index.html` contains the page, phone frame, gallery iframe, and QR card. The iframe loads the [native showcase](https://github.com/otf-kit/ui-native-showcase). This repository has no application build step.

## Contributing

Read [CONTRIBUTING.md](CONTRIBUTING.md) for issue reports and focused changes. The [OTF SDK](https://github.com/otf-kit/sdk) contains the underlying component library.
