# FIGMA_LINKS.md — transaction-detail

<!-- schema: v3.2 | generated: 2026-07-01T11:05:42.131Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [5458150709735075451](https://stitch.google.com/projects/5458150709735075451) |
| Design System ID | 8085591672064527850 |
| Generated | 2026-07-01T11:03:46.934Z |
| Success | 3/3 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | ecf6c906ae834a06920823e21e615545 | 01-transaction-detail-loading | PNG ✅ | HTML ✅ | ✅ generated |
| content | d81afa08a4a94fb78925b1ee88bf67d1 | 02-transaction-detail-content | PNG ✅ | HTML ✅ | ✅ generated |
| error | 998600476df64cafa9273d3b15e354c9 | 03-transaction-detail-error | PNG ✅ | HTML ✅ | ✅ generated |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | [Open](https://stitch.google.com/projects/5458150709735075451/screens/ecf6c906ae834a06920823e21e615545) | — |
| content | [Open](https://stitch.google.com/projects/5458150709735075451/screens/d81afa08a4a94fb78925b1ee88bf67d1) | — |
| error | [Open](https://stitch.google.com/projects/5458150709735075451/screens/998600476df64cafa9273d3b15e354c9) | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features transaction-detail --force
```