# FIGMA_LINKS.md — home

<!-- schema: v3.2 | generated: 2026-05-30T06:58:18.590Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [17153754672098888646](https://stitch.google.com/projects/17153754672098888646) |
| Design System ID | 2005644667042354169 |
| Generated | 2026-05-30T06:58:17.686Z |
| Success | 3/4 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | 881e44779d3542c087d2994c9930b983 | 01-home-loading | PNG ✅ | HTML ✅ | ♻ resumed |
| content | 83d8585747a1489ba3fd2e8ffe473b60 | 02-home-content | PNG ✅ | HTML ✅ | ♻ resumed |
| error | cec9daabc2e74c6c9976b477ec5b403e | 03-home-error | PNG ✅ | HTML ✅ | ♻ resumed |
| empty | — | 04-home-empty | PNG ❌ | HTML ❌ | ❌ StitchError: Tool Call Failed [generate_screen_from_text]: Resource has been exhausted (e.g. check quota). |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | [Open](https://stitch.google.com/projects/17153754672098888646/screens/881e44779d3542c087d2994c9930b983) | — |
| content | [Open](https://stitch.google.com/projects/17153754672098888646/screens/83d8585747a1489ba3fd2e8ffe473b60) | — |
| error | [Open](https://stitch.google.com/projects/17153754672098888646/screens/cec9daabc2e74c6c9976b477ec5b403e) | — |
| empty | — | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features home --force
```