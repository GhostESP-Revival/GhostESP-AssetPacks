## Asset Pack Submission

### Source layout

<!--
Pick one and delete the other.

PNG source: CI runs `gbt asset pack` to convert PNGs in your source repo.
Pre-built .gimg source: CI packages your already-converted .gimg files.
See CONTRIBUTING.md for details.
-->

- [ ] PNG source (CI builds from PNGs)
- [ ] Pre-built `.gimg` source (CI repackages existing gimg files)

### Checklist

- [ ] `manifest.json` is valid and has all required fields
- [ ] `source_repo` points to a public GitHub repository
- [ ] `commit_sha` is a valid commit hash
- [ ] Source builds successfully (via `gbt asset pack --archive .` for PNG sources,
      or contains a valid runtime manifest with `.gimg` payloads for pass-through)
- [ ] Pack is licensed under an open source license
- [ ] ID is unique and doesn't conflict with existing packs
- [ ] Preview screenshot included in source repo (optional; set `preview` in manifest)

### Description

<!-- Brief description of your asset pack -->

### Contents

<!-- What does this pack include? (Icons, Background, Colors, etc.) -->
