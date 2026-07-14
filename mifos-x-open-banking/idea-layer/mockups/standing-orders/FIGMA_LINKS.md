# FIGMA_LINKS.md — standing-orders

<!-- schema: v3.2 | generated: 2026-07-01T11:05:42.131Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [5458150709735075451](https://stitch.google.com/projects/5458150709735075451) |
| Design System ID | 8085591672064527850 |
| Generated | 2026-07-01T11:02:13.272Z |
| Success | 4/4 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | 1adc89c6dd674ebbb94258ea47705f99 | 01-standing-orders-loading | PNG ✅ | HTML ✅ | ✅ generated |
| content | c63cfbceca6e401d8875b266b8229e98 | 02-standing-orders-content | PNG ✅ | HTML ✅ | ✅ generated |
| empty | cd0056e12d5c4bfc8e578af9871a7840 | 03-standing-orders-empty | PNG ✅ | HTML ✅ | ✅ generated |
| error | 73d9cdec0bfd4911a6ba81adb0aa668b | 04-standing-orders-error | PNG ✅ | HTML ✅ | ✅ generated |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | [Open](https://stitch.google.com/projects/5458150709735075451/screens/1adc89c6dd674ebbb94258ea47705f99) | — |
| content | [Open](https://stitch.google.com/projects/5458150709735075451/screens/c63cfbceca6e401d8875b266b8229e98) | — |
| empty | [Open](https://stitch.google.com/projects/5458150709735075451/screens/cd0056e12d5c4bfc8e578af9871a7840) | — |
| error | [Open](https://stitch.google.com/projects/5458150709735075451/screens/73d9cdec0bfd4911a6ba81adb0aa668b) | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features standing-orders --force
```