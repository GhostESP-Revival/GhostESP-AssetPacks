# Contributing to GhostESP Asset Catalog

## How It Works

1. You PR a `manifest.json` pointing to your source repo
2. Maintainers review and merge
3. CI clones your source, builds `.gtheme`, uploads to the CDN
4. Catalog lists the pack using metadata from `manifest.json`

## Manifest Format

Copy `templates/asset-manifest.json` to `assets/<your_pack_id>/manifest.json`:

| Field | Required | Description |
|-------|----------|-------------|
| `id` | Yes | Unique identifier (lowercase, underscores) |
| `name` | Yes | Display name |
| `version` | Yes | Version string |
| `authors` | Yes | Array of author names |
| `category` | Yes | Category (e.g., Theme) |
| `type` | Yes | Must be `"asset"` |
| `description` | Yes | Short description |
| `contents` | No | Array of what's included (Icons, Background, Colors) |
| `license` | Yes | SPDX license identifier |
| `source_repo` | Yes | GitHub URL to your source repo |
| `commit_sha` | Yes | Commit hash with the source to build (so builds are reproducible) |
| `preview` | No | Path (in source) to a PNG preview screenshot; uploaded to the CDN |

## Source Repo Requirements

Your source repo must be a public GitHub repository and contain a valid GhostESP
asset pack. There are two supported source layouts — pick whichever fits your
build pipeline.

### PNG source (built by CI)

The source ships PNG artwork. CI runs `gbt asset pack` to convert them into
`.gimg` payloads.

```
your-asset-pack/
├── manifest.json
├── icons/
│   └── wifi.png
└── bg/
    └── background.png
```

`manifest.json` uses the build-from-source schema:

```json
{
  "id": "my_theme",
  "name": "My Theme",
  "version": "1",
  "authors": ["YourName"],
  "category": "Theme",
  "type": "asset",
  "description": "A cool theme.",
  "contents": ["Icons", "Background", "Colors"],
  "license": "GPL-3.0",
  "source_repo": "https://github.com/YourName/my-ghostesp-theme",
  "commit_sha": "abc123def456",
  "preview": "screenshot.png",
  "reviewed": false
}
```

The runtime manifest inside the source repo (`manifest.json`) must use the
`icon_sources` / `background_sources` sections so the builder knows what PNGs
to convert.

### Pre-built `.gimg` source (pass-through)

The source already contains converted `.gimg` payloads (typically produced
locally with `gbt asset pack`). CI skips PNG conversion and just repackages
the source into a `.gtheme` archive.

```
your-asset-pack/
├── manifest.json
├── icons/
│   └── wifi_l.gimg
│   └── wifi_s.gimg
└── bg/
    └── bg_full.gimg
```

`manifest.json` references the gimg files directly:

```json
{
  "id": "my_theme",
  "backgrounds": {
    "full": "bg/bg_full.gimg"
  },
  "icons": {
    "wifi": {
      "l": "icons/wifi_l.gimg",
      "s": "icons/wifi_s.gimg"
    }
  },
  "colors": {
    "accent": "0x7400E2"
  },
  "format": "ghostesp_asset_pack",
  "version": 1
}
```

The catalog-level manifest in this repo (what you PR) still uses the same
schema as the PNG flow:

```json
{
  "id": "my_theme",
  "name": "My Theme",
  "version": "1",
  "authors": ["YourName"],
  "category": "Theme",
  "type": "asset",
  "description": "A cool theme.",
  "contents": ["Icons", "Background", "Colors"],
  "license": "GPL-3.0",
  "source_repo": "https://github.com/YourName/my-ghostesp-theme",
  "commit_sha": "abc123def456",
  "reviewed": false
}
```

Omit `preview` if you don't want a screenshot hosted on the CDN. CI detects
which source layout to use by inspecting the upstream manifest.

## Local Source

For maintainers adding a pack directly to this repo (instead of an external
`source_repo`), place the asset pack contents in
`assets/<your_pack_id>/source/`. The build script will use that directory
verbatim.

## Updating

Increment the version in your manifest, update `commit_sha` to point to the new
source commit, and open a new PR.

## Rules

- Do not edit `catalog.json` directly - it is auto-generated
- Your source repo must be public
- Respond to review feedback within 14 days
