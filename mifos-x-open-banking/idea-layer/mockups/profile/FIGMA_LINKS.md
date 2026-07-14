# FIGMA_LINKS.md — profile

<!-- schema: v3.2 | generated: 2026-07-01T11:15:41.447Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [5458150709735075451](https://stitch.google.com/projects/5458150709735075451) |
| Design System ID | 8085591672064527850 |
| Generated | 2026-07-01T11:15:41.446Z |
| Success | 0/5 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | — | 01-profile-loading | PNG ❌ | HTML ❌ | ❌ STN gate failure pre-API: STN4: font/size literals not allowed in prompt intro/DONTs/mood-close — typography & spacing come from DESIGN.md: 56dp, 32dp, 96dp, 12dp, 48dp, 180dp, 16dp, 140dp, 80dp, 10dp, 24dp, 200dp, 168dp, 20dp, 160dp, 120dp, 36dp |
| content | — | 02-profile-content | PNG ❌ | HTML ❌ | ❌ STN gate failure pre-API: STN4: font/size literals not allowed in prompt intro/DONTs/mood-close — typography & spacing come from DESIGN.md: 56dp, 32dp, 88dp, 12dp, 48dp, 4dp, 8dp, 36dp, 80dp |
| content_expiring | — | 03-profile-content_expiring | PNG ❌ | HTML ❌ | ❌ STN gate failure pre-API: STN4: font/size literals not allowed in prompt intro/DONTs/mood-close — typography & spacing come from DESIGN.md: 56dp, 32dp, 88dp, 12dp, 48dp, 80dp, 24dp, 36dp, 8dp |
| confirm_sign_out | — | 04-profile-confirm_sign_out | PNG ❌ | HTML ❌ | ❌ STN gate failure pre-API: STN4: font/size literals not allowed in prompt intro/DONTs/mood-close — typography & spacing come from DESIGN.md: 56dp, 32dp, 320dp, 12dp, 24dp, 8dp, 36dp, 80dp |
| error | — | 05-profile-error | PNG ❌ | HTML ❌ | ❌ STN gate failure pre-API: STN4: font/size literals not allowed in prompt intro/DONTs/mood-close — typography & spacing come from DESIGN.md: 56dp, 48dp, 24dp, 80dp |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | — | — |
| content | — | — |
| content_expiring | — | — |
| confirm_sign_out | — | — |
| error | — | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features profile --force
```