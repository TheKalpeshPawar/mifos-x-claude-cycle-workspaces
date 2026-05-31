# FIGMA_LINKS.md — customer-search

<!-- schema: v3.2 | generated: 2026-05-31T05:21:48.074Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [17153754672098888646](https://stitch.google.com/projects/17153754672098888646) |
| Design System ID | 2005644667042354169 |
| Generated | 2026-05-31T05:21:48.074Z |
| Success | 3/4 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| idle | 2b002d2519b44d3da96ed18dc617b047 | 01-customer-search-idle | PNG ✅ | HTML ✅ | ♻ resumed |
| error | 4e18c557f10e494c822519078d00b9b0 | 02-customer-search-error | PNG ✅ | HTML ✅ | ✅ generated |
| content | 6840ae6da32f42aebb840fafa06c2ff6 | 03-customer-search-content | PNG ✅ | HTML ✅ | ✅ generated |
| empty | — | 04-customer-search-empty | PNG ❌ | HTML ❌ | ❌ StitchError: Tool Call Failed [generate_screen_from_text]: The service is currently unavailable. |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| idle | [Open](https://stitch.google.com/projects/17153754672098888646/screens/2b002d2519b44d3da96ed18dc617b047) | — |
| error | [Open](https://stitch.google.com/projects/17153754672098888646/screens/4e18c557f10e494c822519078d00b9b0) | — |
| content | [Open](https://stitch.google.com/projects/17153754672098888646/screens/6840ae6da32f42aebb840fafa06c2ff6) | — |
| empty | — | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features customer-search --force
```