# FIGMA_LINKS.md — settings

<!-- schema: v3.2 | generated: 2026-07-01T11:15:41.447Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [5458150709735075451](https://stitch.google.com/projects/5458150709735075451) |
| Design System ID | 8085591672064527850 |
| Generated | 2026-07-01T11:15:41.446Z |
| Success | 0/2 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | — | 01-settings-loading | PNG ❌ | HTML ❌ | ❌ STN gate failure pre-API: STN4: font/size literals not allowed in prompt intro/DONTs/mood-close — typography & spacing come from DESIGN.md: 56dp, 32dp, 14dp, 52dp, 8dp, 80dp, 48dp |
| content | — | 02-settings-content | PNG ❌ | HTML ❌ | ❌ STN gate failure pre-API: STN4: font/size literals not allowed in prompt intro/DONTs/mood-close — typography & spacing come from DESIGN.md: 56dp, 32dp, 80dp, 48dp |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | — | — |
| content | — | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features settings --force
```