# FIGMA_LINKS.md — pfm-dashboard

<!-- schema: v3.2 | generated: 2026-07-01T11:15:41.447Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [5458150709735075451](https://stitch.google.com/projects/5458150709735075451) |
| Design System ID | 8085591672064527850 |
| Generated | 2026-07-01T11:15:41.446Z |
| Success | 0/4 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | — | 01-pfm-dashboard-loading | PNG ❌ | HTML ❌ | ❌ STN gate failure pre-API: STN4: font/size literals not allowed in prompt intro/DONTs/mood-close — typography & spacing come from DESIGN.md: 56dp, 32dp, 40dp, 88dp, 36dp, 128dp, 12dp, 200dp, 20dp, 120dp, 100dp, 8dp, 180dp, 160dp, 14dp, 80dp, 10dp, 48dp, 140dp |
| content | — | 02-pfm-dashboard-content | PNG ❌ | HTML ❌ | ❌ STN gate failure pre-API: STN4: font/size literals not allowed in prompt intro/DONTs/mood-close — typography & spacing come from DESIGN.md: 56dp, 32dp, 40dp, 36dp, 8dp, 132dp, 12dp, 200dp, 48dp, 24dp, 80dp |
| empty | — | 03-pfm-dashboard-empty | PNG ❌ | HTML ❌ | ❌ STN gate failure pre-API: STN4: font/size literals not allowed in prompt intro/DONTs/mood-close — typography & spacing come from DESIGN.md: 56dp, 32dp, 40dp, 36dp, 64dp, 48dp, 24dp, 80dp |
| error | — | 04-pfm-dashboard-error | PNG ❌ | HTML ❌ | ❌ STN gate failure pre-API: STN4: font/size literals not allowed in prompt intro/DONTs/mood-close — typography & spacing come from DESIGN.md: 56dp, 32dp, 40dp, 36dp, 48dp, 24dp, 80dp |

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
  --workspace mifos-x/mifos-x-open-banking --features pfm-dashboard --force
```