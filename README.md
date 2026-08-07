# Stanford Sites Hotfix

A minimal Sass build that compiles a single stylesheet and publishes it to GitHub Pages:

https://su-sws.github.io/stanford-sites-hotfix/style.css

## Requirements

- Node.js 24
- Yarn 4 (Berry) via [Corepack](https://nodejs.org/api/corepack.html)

## Getting started

```bash
corepack enable
yarn install --immutable
```

## Development

```bash
yarn watch
```

Watches `scss/style.scss` and recompiles to `css/style.css` on every change.

## Build

```bash
yarn build
```

Compiles `scss/style.scss` to `css/style.css`, compressed with no source map. This is the same command CI runs before deploying.

## Project structure

- `scss/style.scss` — source Sass file.
- `css/` — build output (git-ignored, not committed).
- `robots.txt` — blocks search engine crawlers on the published Pages site.

## Deployment

Pushing to `main` triggers `.github/workflows/deploy.yml`, which builds the CSS and publishes the `css/` directory to GitHub Pages. There is no staging step, so anything merged to `main` goes live immediately.
