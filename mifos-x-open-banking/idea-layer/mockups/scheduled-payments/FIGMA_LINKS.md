# FIGMA_LINKS.md — scheduled-payments

<!-- schema: v3.2 | generated: 2026-07-01T10:59:44.534Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [5458150709735075451](https://stitch.google.com/projects/5458150709735075451) |
| Design System ID | 8085591672064527850 |
| Generated | 2026-07-01T10:59:33.096Z |
| Success | 4/4 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | ba2f07954da646eca3e6cf706107e60f | 01-scheduled-payments-loading | PNG ✅ | HTML ✅ | ✅ generated |
| content | 8eb596b756474c6491f58a0932973843 | 02-scheduled-payments-content | PNG ✅ | HTML ✅ | ✅ generated |
| empty | 2e8fc6a1f1fd405796b17d9c5c096056 | 03-scheduled-payments-empty | PNG ✅ | HTML ✅ | ✅ generated |
| error | 82caee273c1149eda345c8c7777a71ea | 04-scheduled-payments-error | PNG ✅ | HTML ✅ | ✅ generated |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | [Open](https://stitch.google.com/projects/5458150709735075451/screens/ba2f07954da646eca3e6cf706107e60f) | — |
| content | [Open](https://stitch.google.com/projects/5458150709735075451/screens/8eb596b756474c6491f58a0932973843) | — |
| empty | [Open](https://stitch.google.com/projects/5458150709735075451/screens/2e8fc6a1f1fd405796b17d9c5c096056) | — |
| error | [Open](https://stitch.google.com/projects/5458150709735075451/screens/82caee273c1149eda345c8c7777a71ea) | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features scheduled-payments --force
```