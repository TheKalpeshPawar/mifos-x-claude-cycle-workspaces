# FIGMA_LINKS.md — transactions

<!-- schema: v3.2 | generated: 2026-07-01T11:05:42.131Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [5458150709735075451](https://stitch.google.com/projects/5458150709735075451) |
| Design System ID | 8085591672064527850 |
| Generated | 2026-07-01T11:05:28.761Z |
| Success | 4/4 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | 583740e6e4394f4db49190241ee94fa2 | 01-transactions-loading | PNG ✅ | HTML ✅ | ✅ generated |
| content | b6564f7fafac4e4c9c997c80260cbc07 | 02-transactions-content | PNG ✅ | HTML ✅ | ✅ generated |
| empty | 7a492d82b2ab40db830268c3612d752e | 03-transactions-empty | PNG ✅ | HTML ✅ | ✅ generated |
| error | a419114dd30c4e86971b73406f548087 | 04-transactions-error | PNG ✅ | HTML ✅ | ✅ generated |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | [Open](https://stitch.google.com/projects/5458150709735075451/screens/583740e6e4394f4db49190241ee94fa2) | — |
| content | [Open](https://stitch.google.com/projects/5458150709735075451/screens/b6564f7fafac4e4c9c997c80260cbc07) | — |
| empty | [Open](https://stitch.google.com/projects/5458150709735075451/screens/7a492d82b2ab40db830268c3612d752e) | — |
| error | [Open](https://stitch.google.com/projects/5458150709735075451/screens/a419114dd30c4e86971b73406f548087) | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features transactions --force
```