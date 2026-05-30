# FIGMA_LINKS.md — customer-detail

<!-- schema: v3.2 | generated: 2026-05-30T05:57:49.185Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [17153754672098888646](https://stitch.google.com/projects/17153754672098888646) |
| Design System ID | 2005644667042354169 |
| Generated | 2026-05-30T05:57:49.185Z |
| Success | 4/4 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | ef7c4b1b846e49659f56a579b153c66b | 01-customer-detail-loading | PNG ✅ | HTML ✅ | ♻ resumed |
| content | 079b64e94f3c4df4b5c8355c75cae0a8 | 02-customer-detail-content | PNG ✅ | HTML ✅ | ♻ resumed |
| error | 0296eddf40984d9ca95287d3ece32b70 | 03-customer-detail-error | PNG ✅ | HTML ✅ | ✅ generated |
| empty | bbb774ada2134ee7a020e1edb5e95f62 | 04-customer-detail-empty | PNG ✅ | HTML ✅ | ✅ generated |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | [Open](https://stitch.google.com/projects/17153754672098888646/screens/ef7c4b1b846e49659f56a579b153c66b) | — |
| content | [Open](https://stitch.google.com/projects/17153754672098888646/screens/079b64e94f3c4df4b5c8355c75cae0a8) | — |
| error | [Open](https://stitch.google.com/projects/17153754672098888646/screens/0296eddf40984d9ca95287d3ece32b70) | — |
| empty | [Open](https://stitch.google.com/projects/17153754672098888646/screens/bbb774ada2134ee7a020e1edb5e95f62) | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features customer-detail --force
```