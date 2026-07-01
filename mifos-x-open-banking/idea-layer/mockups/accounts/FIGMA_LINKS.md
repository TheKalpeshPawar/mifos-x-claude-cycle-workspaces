# FIGMA_LINKS.md — accounts

<!-- schema: v3.2 | generated: 2026-07-01T04:11:53.901Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [5458150709735075451](https://stitch.google.com/projects/5458150709735075451) |
| Design System ID | 8085591672064527850 |
| Generated | 2026-07-01T04:11:53.901Z |
| Success | 5/5 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | 37e2657f372a4463acd2b04b0209451b | 01-accounts-loading | PNG ✅ | HTML ✅ | ✅ generated |
| content | 007a7533a9194726979bc78898a85ca9 | 02-accounts-content | PNG ✅ | HTML ✅ | ✅ generated |
| consent_expiring | 8a3ee954b7344c208f01d38a7e755b10 | 03-accounts-consent_expiring | PNG ✅ | HTML ✅ | ✅ generated |
| empty | ef99ff6c63f44496932fa3782e2d19d1 | 04-accounts-empty | PNG ✅ | HTML ✅ | ✅ generated |
| error | 520321dae731460b8be2ad2b8e40d6a6 | 05-accounts-error | PNG ✅ | HTML ✅ | ✅ generated |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | [Open](https://stitch.google.com/projects/5458150709735075451/screens/37e2657f372a4463acd2b04b0209451b) | — |
| content | [Open](https://stitch.google.com/projects/5458150709735075451/screens/007a7533a9194726979bc78898a85ca9) | — |
| consent_expiring | [Open](https://stitch.google.com/projects/5458150709735075451/screens/8a3ee954b7344c208f01d38a7e755b10) | — |
| empty | [Open](https://stitch.google.com/projects/5458150709735075451/screens/ef99ff6c63f44496932fa3782e2d19d1) | — |
| error | [Open](https://stitch.google.com/projects/5458150709735075451/screens/520321dae731460b8be2ad2b8e40d6a6) | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features accounts --force
```