# FIGMA_LINKS.md — statement-detail

<!-- schema: v3.2 | generated: 2026-07-01T11:05:42.131Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [5458150709735075451](https://stitch.google.com/projects/5458150709735075451) |
| Design System ID | 8085591672064527850 |
| Generated | 2026-07-01T11:05:42.131Z |
| Success | 4/4 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | 824f4a8c50d04d8b9664be833d210f84 | 01-statement-detail-loading | PNG ✅ | HTML ✅ | ✅ generated |
| content | 1e45ea5817084f01875180ef6d182b83 | 02-statement-detail-content | PNG ✅ | HTML ✅ | ✅ generated |
| empty | a1e4d03971854143b709b7cbd549b639 | 03-statement-detail-empty | PNG ✅ | HTML ✅ | ✅ generated |
| error | cccdb01ad3fd41579aab6efb055876ab | 04-statement-detail-error | PNG ✅ | HTML ✅ | ✅ generated |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | [Open](https://stitch.google.com/projects/5458150709735075451/screens/824f4a8c50d04d8b9664be833d210f84) | — |
| content | [Open](https://stitch.google.com/projects/5458150709735075451/screens/1e45ea5817084f01875180ef6d182b83) | — |
| empty | [Open](https://stitch.google.com/projects/5458150709735075451/screens/a1e4d03971854143b709b7cbd549b639) | — |
| error | [Open](https://stitch.google.com/projects/5458150709735075451/screens/cccdb01ad3fd41579aab6efb055876ab) | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features statement-detail --force
```