# FIGMA_LINKS.md — atm-locator

<!-- schema: v3.2 | generated: 2026-07-01T10:51:08.363Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [5458150709735075451](https://stitch.google.com/projects/5458150709735075451) |
| Design System ID | 8085591672064527850 |
| Generated | 2026-07-01T10:50:58.664Z |
| Success | 4/4 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | fbf33adaf29c457bb99751e8699e84cd | 01-atm-locator-loading | PNG ✅ | HTML ✅ | ✅ generated |
| content | 260c973cfe3749b6b0b09c0eac7043fe | 02-atm-locator-content | PNG ✅ | HTML ✅ | ✅ generated |
| empty | 63c8c9ec18b04a64b56d6eb8272126e7 | 03-atm-locator-empty | PNG ✅ | HTML ✅ | ✅ generated |
| error | 9c2f37b74f664bc3acca6a0e9e50e0ab | 04-atm-locator-error | PNG ✅ | HTML ✅ | ✅ generated |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | [Open](https://stitch.google.com/projects/5458150709735075451/screens/fbf33adaf29c457bb99751e8699e84cd) | — |
| content | [Open](https://stitch.google.com/projects/5458150709735075451/screens/260c973cfe3749b6b0b09c0eac7043fe) | — |
| empty | [Open](https://stitch.google.com/projects/5458150709735075451/screens/63c8c9ec18b04a64b56d6eb8272126e7) | — |
| error | [Open](https://stitch.google.com/projects/5458150709735075451/screens/9c2f37b74f664bc3acca6a0e9e50e0ab) | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features atm-locator --force
```