# FIGMA_LINKS.md — login

<!-- schema: v3.2 | generated: 2026-07-01T10:52:41.601Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [5458150709735075451](https://stitch.google.com/projects/5458150709735075451) |
| Design System ID | 8085591672064527850 |
| Generated | 2026-07-01T10:52:41.600Z |
| Success | 4/4 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| content | 73d8b20312044d6288cdb22b657331c2 | 01-login-content | PNG ❌ | HTML ❌ | ✅ generated |
| loading | 7df39255b7bd478584defac66ccd2248 | 02-login-loading | PNG ✅ | HTML ✅ | ✅ generated |
| authorising | 264660d3c245476bac0fec5c4b24893e | 03-login-authorising | PNG ✅ | HTML ✅ | ✅ generated |
| error | cc4c7a4a1e614883b456408c74c0dcae | 04-login-error | PNG ✅ | HTML ✅ | ✅ generated |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| content | [Open](https://stitch.google.com/projects/5458150709735075451/screens/73d8b20312044d6288cdb22b657331c2) | — |
| loading | [Open](https://stitch.google.com/projects/5458150709735075451/screens/7df39255b7bd478584defac66ccd2248) | — |
| authorising | [Open](https://stitch.google.com/projects/5458150709735075451/screens/264660d3c245476bac0fec5c4b24893e) | — |
| error | [Open](https://stitch.google.com/projects/5458150709735075451/screens/cc4c7a4a1e614883b456408c74c0dcae) | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features login --force
```