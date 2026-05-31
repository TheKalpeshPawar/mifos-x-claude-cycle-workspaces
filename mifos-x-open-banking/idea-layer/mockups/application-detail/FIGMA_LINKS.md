# FIGMA_LINKS.md — application-detail

<!-- schema: v3.2 | generated: 2026-05-31T03:38:44.519Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [17153754672098888646](https://stitch.google.com/projects/17153754672098888646) |
| Design System ID | 2005644667042354169 |
| Generated | 2026-05-31T03:38:01.164Z |
| Success | 7/7 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | 798a55d1a73a413e9ab336c8bd90ef4b | 01-application-detail-loading | PNG ✅ | HTML ✅ | ✅ generated |
| reviewing | 3eef9d34746d4c7789f19278b56d60a2 | 02-application-detail-reviewing | PNG ✅ | HTML ✅ | ✅ generated |
| approved | ea54326ff95b4f3f8803f930c0a04586 | 03-application-detail-approved | PNG ✅ | HTML ✅ | ✅ generated |
| rejected | 62df5da6e50349f1ac5ae7acd1060c24 | 04-application-detail-rejected | PNG ✅ | HTML ✅ | ✅ generated |
| content | e64adab08ecf4780b49bb62995d4683f | 05-application-detail-content | PNG ✅ | HTML ✅ | ✅ generated |
| empty | ae24bf9da84f450ba757c851998f346e | 06-application-detail-empty | PNG ✅ | HTML ✅ | ✅ generated |
| error | 533c7aa3c5ea439f8c2aa585e860dd13 | 07-application-detail-error | PNG ✅ | HTML ✅ | ✅ generated |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | [Open](https://stitch.google.com/projects/17153754672098888646/screens/798a55d1a73a413e9ab336c8bd90ef4b) | — |
| reviewing | [Open](https://stitch.google.com/projects/17153754672098888646/screens/3eef9d34746d4c7789f19278b56d60a2) | — |
| approved | [Open](https://stitch.google.com/projects/17153754672098888646/screens/ea54326ff95b4f3f8803f930c0a04586) | — |
| rejected | [Open](https://stitch.google.com/projects/17153754672098888646/screens/62df5da6e50349f1ac5ae7acd1060c24) | — |
| content | [Open](https://stitch.google.com/projects/17153754672098888646/screens/e64adab08ecf4780b49bb62995d4683f) | — |
| empty | [Open](https://stitch.google.com/projects/17153754672098888646/screens/ae24bf9da84f450ba757c851998f346e) | — |
| error | [Open](https://stitch.google.com/projects/17153754672098888646/screens/533c7aa3c5ea439f8c2aa585e860dd13) | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features application-detail --force
```