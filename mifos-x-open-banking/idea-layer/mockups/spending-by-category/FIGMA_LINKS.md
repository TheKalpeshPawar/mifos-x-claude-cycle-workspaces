# FIGMA_LINKS.md — spending-by-category

<!-- schema: v3.2 | generated: 2026-07-01T10:59:44.534Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [5458150709735075451](https://stitch.google.com/projects/5458150709735075451) |
| Design System ID | 8085591672064527850 |
| Generated | 2026-07-01T10:59:44.533Z |
| Success | 4/4 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | ec500293be2248c7a0ee0ae70041a3f2 | 01-spending-by-category-loading | PNG ✅ | HTML ✅ | ✅ generated |
| content | 465c881bc49a4336a26c38fec6b1c6b9 | 02-spending-by-category-content | PNG ✅ | HTML ✅ | ✅ generated |
| empty | 18e4ef64017f4338ba58e9f191342b97 | 03-spending-by-category-empty | PNG ✅ | HTML ✅ | ✅ generated |
| error | b72d848aa1eb46569e4c74fbe4bdded0 | 04-spending-by-category-error | PNG ✅ | HTML ✅ | ✅ generated |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | [Open](https://stitch.google.com/projects/5458150709735075451/screens/ec500293be2248c7a0ee0ae70041a3f2) | — |
| content | [Open](https://stitch.google.com/projects/5458150709735075451/screens/465c881bc49a4336a26c38fec6b1c6b9) | — |
| empty | [Open](https://stitch.google.com/projects/5458150709735075451/screens/18e4ef64017f4338ba58e9f191342b97) | — |
| error | [Open](https://stitch.google.com/projects/5458150709735075451/screens/b72d848aa1eb46569e4c74fbe4bdded0) | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features spending-by-category --force
```