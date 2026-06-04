# GhostESP Asset Catalog

Community-driven catalog for GhostESP asset packs (`.gtheme`).

## How It Works

1. **Contributors** submit asset packs via Pull Request
2. **Maintainers** review and merge PRs
3. **CI automatically** builds `.gtheme` files with `gbt asset pack` and uploads to Cloudflare R2 CDN
4. **The website** fetches `catalog.json` to display asset packs

## Submitting an Asset Pack

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed instructions.

Quick start:
1. Fork this repo
2. Copy `templates/asset-manifest.json` to `assets/<your_pack_id>/manifest.json`
3. Put your source files (manifest.json, PNGs) in `assets/<your_pack_id>/source/`
4. Open a Pull Request

## CDN

All built `.gtheme` files are hosted on Cloudflare R2 at `https://gesp.fuckyourcdn.com`.
