# FIGMA_LINKS.md — transaction-tags

<!-- schema: v3.2 | generated: 2026-05-30T06:58:19.587Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [17153754672098888646](https://stitch.google.com/projects/17153754672098888646) |
| Design System ID | 2005644667042354169 |
| Generated | 2026-05-30T06:58:19.587Z |
| Success | 6/7 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | d89234aa6d21452194e9ebe5bb39784c | 01-transaction-tags-loading | PNG ✅ | HTML ✅ | ♻ resumed |
| view_tags | 2e34e6fce2ec4b7eac62632fdf3d59fc | 02-transaction-tags-view_tags | PNG ✅ | HTML ✅ | ♻ resumed |
| edit_mode | 83ed0b70a2414350998cd4c63507e4dc | 03-transaction-tags-edit_mode | PNG ✅ | HTML ✅ | ♻ resumed |
| save_success | 7e7f0348b7d043f381a73340384e7f0f | 04-transaction-tags-save_success | PNG ✅ | HTML ✅ | ♻ resumed |
| content | 854a91946b9341e7b1e968d661aaaecf | 05-transaction-tags-content | PNG ✅ | HTML ✅ | ♻ resumed |
| empty | 8398b08cc15842859005b0c408fe1d6c | 06-transaction-tags-empty | PNG ✅ | HTML ✅ | ♻ resumed |
| error | — | 07-transaction-tags-error | PNG ❌ | HTML ❌ | ❌ StitchError: Tool Call Failed [generate_screen_from_text]: Resource has been exhausted (e.g. check quota). |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | [Open](https://stitch.google.com/projects/17153754672098888646/screens/d89234aa6d21452194e9ebe5bb39784c) | — |
| view_tags | [Open](https://stitch.google.com/projects/17153754672098888646/screens/2e34e6fce2ec4b7eac62632fdf3d59fc) | — |
| edit_mode | [Open](https://stitch.google.com/projects/17153754672098888646/screens/83ed0b70a2414350998cd4c63507e4dc) | — |
| save_success | [Open](https://stitch.google.com/projects/17153754672098888646/screens/7e7f0348b7d043f381a73340384e7f0f) | — |
| content | [Open](https://stitch.google.com/projects/17153754672098888646/screens/854a91946b9341e7b1e968d661aaaecf) | — |
| empty | [Open](https://stitch.google.com/projects/17153754672098888646/screens/8398b08cc15842859005b0c408fe1d6c) | — |
| error | — | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features transaction-tags --force
```