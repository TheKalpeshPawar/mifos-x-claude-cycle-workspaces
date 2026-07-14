# FIGMA_LINKS.md — beneficiaries

<!-- schema: v3.2 | generated: 2026-07-01T10:51:08.363Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [5458150709735075451](https://stitch.google.com/projects/5458150709735075451) |
| Design System ID | 8085591672064527850 |
| Generated | 2026-07-01T10:51:01.469Z |
| Success | 4/4 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | 5f940473016948fb8463d943dcceb52c | 01-beneficiaries-loading | PNG ✅ | HTML ✅ | ✅ generated |
| content | fe02997a233b4fe984697531bb561c14 | 02-beneficiaries-content | PNG ✅ | HTML ✅ | ✅ generated |
| empty | d7a69e5973364f87b72c029dd1055243 | 03-beneficiaries-empty | PNG ✅ | HTML ✅ | ✅ generated |
| error | 95f80bf1796f4799b3f904298bb926eb | 04-beneficiaries-error | PNG ✅ | HTML ✅ | ✅ generated |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | [Open](https://stitch.google.com/projects/5458150709735075451/screens/5f940473016948fb8463d943dcceb52c) | — |
| content | [Open](https://stitch.google.com/projects/5458150709735075451/screens/fe02997a233b4fe984697531bb561c14) | — |
| empty | [Open](https://stitch.google.com/projects/5458150709735075451/screens/d7a69e5973364f87b72c029dd1055243) | — |
| error | [Open](https://stitch.google.com/projects/5458150709735075451/screens/95f80bf1796f4799b3f904298bb926eb) | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features beneficiaries --force
```