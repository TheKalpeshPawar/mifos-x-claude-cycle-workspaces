# FIGMA_LINKS.md — statements

<!-- schema: v3.2 | generated: 2026-07-01T11:17:03.843Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [5458150709735075451](https://stitch.google.com/projects/5458150709735075451) |
| Design System ID | 8085591672064527850 |
| Generated | 2026-07-01T11:17:03.843Z |
| Success | 2/4 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | — | 01-statements-loading | PNG ❌ | HTML ❌ | ❌ STN gate failure pre-API: STN4: font/size literals not allowed in prompt intro/DONTs/mood-close — typography & spacing come from DESIGN.md: 72dp |
| content | — | 02-statements-content | PNG ❌ | HTML ❌ | ❌ STN gate failure pre-API: STN4: font/size literals not allowed in prompt intro/DONTs/mood-close — typography & spacing come from DESIGN.md: 1dp |
| empty | 657661741e3a40b5ad572b0162804e6a | 03-statements-empty | PNG ✅ | HTML ✅ | ✅ generated |
| error | 40afa7418f034735bd6a267bd5f5ef70 | 04-statements-error | PNG ✅ | HTML ✅ | ✅ generated |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | — | — |
| content | — | — |
| empty | [Open](https://stitch.google.com/projects/5458150709735075451/screens/657661741e3a40b5ad572b0162804e6a) | — |
| error | [Open](https://stitch.google.com/projects/5458150709735075451/screens/40afa7418f034735bd6a267bd5f5ef70) | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features statements --force
```