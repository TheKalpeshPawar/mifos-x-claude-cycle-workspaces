# FIGMA_LINKS.md — home

<!-- schema: v3.2 | generated: 2026-05-29T17:13:15.021Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [17153754672098888646](https://stitch.google.com/projects/17153754672098888646) |
| Design System ID | 2005644667042354169 |
| Generated | 2026-05-29T17:13:13.579Z |
| Success | 0/4 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | — | 01-home-loading | PNG ❌ | HTML ❌ | ❌ STN gate failure pre-API: STN2: prompt is 4636 chars (cap 4000) — apply the shrink ladder or split the screen |
| content | — | 02-home-content | PNG ❌ | HTML ❌ | ❌ STN gate failure pre-API: STN2: prompt is 5403 chars (cap 4000) — apply the shrink ladder or split the screen |
| error | — | 03-home-error | PNG ❌ | HTML ❌ | ❌ STN gate failure pre-API: STN2: prompt is 4437 chars (cap 4000) — apply the shrink ladder or split the screen |
| empty | — | 04-home-empty | PNG ❌ | HTML ❌ | ❌ STN gate failure pre-API: STN2: prompt is 4306 chars (cap 4000) — apply the shrink ladder or split the screen |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | — | — |
| content | — | — |
| error | — | — |
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