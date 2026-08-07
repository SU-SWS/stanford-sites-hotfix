# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A minimal SCSS build that compiles `scss/style.scss` to `css/style.css` and publishes the `css/` directory to GitHub Pages. There is no application code, no JS bundling, and no test suite — the entire purpose of the repo is the compiled stylesheet.

## Commands

- `yarn build` — compile `scss/style.scss` → `css/style.css`, compressed, no source map (this is what CI runs).
- `yarn watch` — recompile on change during local development.

Uses Yarn 4 (Berry) with `nodeLinker: node-modules` (see `.yarnrc.yml`); run `corepack enable` first if `yarn` resolves to the wrong version. Install deps with `yarn install --immutable` to match CI.

## Architecture

- `scss/style.scss` is the single source SCSS file (variables + rules; no partials/imports currently exist, but future additions would follow standard Sass `@use`/partial conventions).
- `css/` is a git-ignored build output directory, not checked into version control. It also holds `robots.txt`, copied there only during the CI deploy step (see below) — `css/robots.txt` will not exist locally after just running `yarn build`.
- `robots.txt` at the repo root blocks all crawlers (`Disallow: /`) since this deploys to a public GitHub Pages URL that isn't meant to be indexed.

## Deployment (`.github/workflows/deploy.yml`)

On every push to `main`: installs deps, runs `yarn build`, copies `robots.txt` into `css/`, then deploys the `css/` directory as a GitHub Pages artifact. There is no PR preview or staging step — anything merged to `main` goes live immediately.
