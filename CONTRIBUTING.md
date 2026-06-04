# Contributing to GhostESP Asset Catalog

## Requirements

1. **Open Source License** - Asset packs must be licensed under an open source license
2. **Unique ID** - Your asset ID must not conflict with existing entries
3. **Valid source** - Your source must build successfully with `gbt asset pack`

## Submitting an Asset Pack

### Step 1: Prepare your source files

Your source directory should contain a `manifest.json` and the PNG assets it references. It should build with:
```bash
gbt asset pack --archive your_pack/source/
```

### Step 2: Create your manifest

Copy `templates/asset-manifest.json` to `assets/<your_pack_id>/manifest.json` and fill in all fields:

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

### Step 3: Add your source files

Place your source files in `assets/<your_pack_id>/source/`:
- `manifest.json` (the gbt manifest with colors, icon_sources, etc.)
- PNG files for icons and backgrounds

### Step 4: Open a Pull Request

1. Fork this repository
2. Create a branch
3. Commit your changes
4. Open a PR against `main`

## Rules

- Do not edit `catalog.json` directly - it is auto-generated
- Do not commit binary `.gtheme` files - they are built by CI
