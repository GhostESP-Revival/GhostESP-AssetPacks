# Contributing to GhostESP Asset Catalog

## How It Works

1. You PR a `manifest.json` pointing to your source repo
2. Maintainers review and merge
3. CI clones your source, builds `.gtheme` with `gbt`, uploads to R2 CDN

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

## Source Repo Requirements

Your source repo must:
1. Contain a valid `gbt` asset pack (manifest.json + PNG files)
2. Build successfully with `gbt asset pack --archive .`
3. Be a public GitHub repository

## Example

```
assets/my_theme/
└── manifest.json    # Points to your external source repo
```

Your manifest.json:
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

## Updating

Increment the version in your manifest, update `commit_sha` to point to the new source commit, and open a new PR.

## Rules

- Do not edit `catalog.json` directly - it is auto-generated
- Your source repo must be public
- Respond to review feedback within 14 days
