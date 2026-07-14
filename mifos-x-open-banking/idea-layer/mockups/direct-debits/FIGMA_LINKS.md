# FIGMA_LINKS.md — direct-debits

<!-- schema: v3.2 | generated: 2026-07-01T10:52:41.601Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [5458150709735075451](https://stitch.google.com/projects/5458150709735075451) |
| Design System ID | 8085591672064527850 |
| Generated | 2026-07-01T10:52:34.235Z |
| Success | 4/4 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | e353f73e0f854b148f514485e5d0fd0f | 01-direct-debits-loading | PNG ✅ | HTML ✅ | ✅ generated |
| content | e3e07cd0ce5142d28deb2e8cdade7031 | 02-direct-debits-content | PNG ✅ | HTML ✅ | ✅ generated |
| empty | be97b39084e44461a0066ee40810d405 | 03-direct-debits-empty | PNG ✅ | HTML ✅ | ✅ generated |
| error | ffc203eb1d4a422facb112fc104baee1 | 04-direct-debits-error | PNG ✅ | HTML ✅ | ✅ generated |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | [Open](https://stitch.google.com/projects/5458150709735075451/screens/e353f73e0f854b148f514485e5d0fd0f) | — |
| content | [Open](https://stitch.google.com/projects/5458150709735075451/screens/e3e07cd0ce5142d28deb2e8cdade7031) | — |
| empty | [Open](https://stitch.google.com/projects/5458150709735075451/screens/be97b39084e44461a0066ee40810d405) | — |
| error | [Open](https://stitch.google.com/projects/5458150709735075451/screens/ffc203eb1d4a422facb112fc104baee1) | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features direct-debits --force
```