# GhostESP Asset Catalog

Community-driven catalog for GhostESP asset packs (`.gtheme`).

## How It Works

1. **Contributors** PR a manifest pointing to their source repo
2. **Maintainers** review and merge
3. **CI** clones source, builds `.gtheme` with `gbt`, uploads to Cloudflare R2
4. **Website** fetches `catalog.json` to display asset packs

## Submitting an Asset Pack

See [CONTRIBUTING.md](CONTRIBUTING.md).

Quick start:
1. Fork this repo
2. Copy `templates/asset-manifest.json` to `assets/<your_pack_id>/manifest.json`
3. Fill in `source_repo` (your public GitHub repo) and `commit_sha`
4. Open a Pull Request

## CDN

Built `.gtheme` files are hosted at `https://gesp.fuckyourcdn.com`.
