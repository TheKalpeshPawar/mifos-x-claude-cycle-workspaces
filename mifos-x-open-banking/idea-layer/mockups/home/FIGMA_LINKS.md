# FIGMA_LINKS.md — home

<!-- schema: v3.2 | generated: 2026-07-01T10:52:41.601Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [5458150709735075451](https://stitch.google.com/projects/5458150709735075451) |
| Design System ID | 8085591672064527850 |
| Generated | 2026-07-01T10:52:31.086Z |
| Success | 4/4 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | 55ba92ca511345508615f480e9e01444 | 01-home-loading | PNG ✅ | HTML ✅ | ✅ generated |
| content | 314a25d9b98b44a8b55a2e60924a916c | 02-home-content | PNG ✅ | HTML ✅ | ✅ generated |
| empty | 376f26ba9b0a457b9d0af9e840acbed7 | 03-home-empty | PNG ✅ | HTML ✅ | ✅ generated |
| error | 7617061b9f3c456fbe8e62d21aedbae9 | 04-home-error | PNG ✅ | HTML ❌ | ✅ generated |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | [Open](https://stitch.google.com/projects/5458150709735075451/screens/55ba92ca511345508615f480e9e01444) | — |
| content | [Open](https://stitch.google.com/projects/5458150709735075451/screens/314a25d9b98b44a8b55a2e60924a916c) | — |
| empty | [Open](https://stitch.google.com/projects/5458150709735075451/screens/376f26ba9b0a457b9d0af9e840acbed7) | — |
| error | [Open](https://stitch.google.com/projects/5458150709735075451/screens/7617061b9f3c456fbe8e62d21aedbae9) | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features home --force
```