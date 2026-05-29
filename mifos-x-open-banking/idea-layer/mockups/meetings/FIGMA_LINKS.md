# FIGMA_LINKS.md — meetings

<!-- schema: v3.2 | generated: 2026-05-29T17:13:16.345Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [17153754672098888646](https://stitch.google.com/projects/17153754672098888646) |
| Design System ID | 2005644667042354169 |
| Generated | 2026-05-29T17:13:15.075Z |
| Success | 0/4 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | — | 01-meetings-loading | PNG ❌ | HTML ❌ | ❌ STN gate failure pre-API: STN2: prompt is 7556 chars (cap 4000) — apply the shrink ladder or split the screen |
| content | — | 02-meetings-content | PNG ❌ | HTML ❌ | ❌ STN gate failure pre-API: STN2: prompt is 5677 chars (cap 4000) — apply the shrink ladder or split the screen |
| empty | — | 03-meetings-empty | PNG ❌ | HTML ❌ | ❌ STN gate failure pre-API: STN2: prompt is 7797 chars (cap 4000) — apply the shrink ladder or split the screen |
| error | — | 04-meetings-error | PNG ❌ | HTML ❌ | ❌ STN gate failure pre-API: STN2: prompt is 7863 chars (cap 4000) — apply the shrink ladder or split the screen |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | — | — |
| content | — | — |
| empty | — | — |
| error | — | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features meetings --force
```