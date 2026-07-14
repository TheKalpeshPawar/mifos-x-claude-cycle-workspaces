# FIGMA_LINKS.md — account-detail

<!-- schema: v3.2 | generated: 2026-07-01T10:51:08.363Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [5458150709735075451](https://stitch.google.com/projects/5458150709735075451) |
| Design System ID | 8085591672064527850 |
| Generated | 2026-07-01T10:51:01.343Z |
| Success | 4/4 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | 9a8526a2afd04019a9cf871c6cf185d3 | 01-account-detail-loading | PNG ✅ | HTML ✅ | ✅ generated |
| content | 3ea3d2161e4f4de8a3e967e56e9b92bc | 02-account-detail-content | PNG ✅ | HTML ✅ | ✅ generated |
| empty | d0c0186a366148a293b3705a92be5f27 | 03-account-detail-empty | PNG ✅ | HTML ✅ | ✅ generated |
| error | 43e8237f7e8647d1a54f5da15db5ec6f | 04-account-detail-error | PNG ✅ | HTML ✅ | ✅ generated |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | [Open](https://stitch.google.com/projects/5458150709735075451/screens/9a8526a2afd04019a9cf871c6cf185d3) | — |
| content | [Open](https://stitch.google.com/projects/5458150709735075451/screens/3ea3d2161e4f4de8a3e967e56e9b92bc) | — |
| empty | [Open](https://stitch.google.com/projects/5458150709735075451/screens/d0c0186a366148a293b3705a92be5f27) | — |
| error | [Open](https://stitch.google.com/projects/5458150709735075451/screens/43e8237f7e8647d1a54f5da15db5ec6f) | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features account-detail --force
```