# FIGMA_LINKS.md — cards

<!-- schema: v3.2 | generated: 2026-05-29T17:13:09.192Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [17153754672098888646](https://stitch.google.com/projects/17153754672098888646) |
| Design System ID | 2005644667042354169 |
| Generated | 2026-05-29T17:13:08.182Z |
| Success | 3/4 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | dbbeb8cb970f46cf9ca004631b5290e1 | 01-cards-loading | PNG ✅ | HTML ✅ | ♻ resumed |
| content | 6891ac9174894c73b66ecbca93715637 | 02-cards-content | PNG ✅ | HTML ✅ | ♻ resumed |
| empty | ed53b321004d4b78ba1512f206943440 | 03-cards-empty | PNG ✅ | HTML ✅ | ♻ resumed |
| error | — | 04-cards-error | PNG ❌ | HTML ❌ | ❌ StitchError: Tool Call Failed [generate_screen_from_text]: Resource has been exhausted (e.g. check quota). |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | [Open](https://stitch.google.com/projects/17153754672098888646/screens/dbbeb8cb970f46cf9ca004631b5290e1) | — |
| content | [Open](https://stitch.google.com/projects/17153754672098888646/screens/6891ac9174894c73b66ecbca93715637) | — |
| empty | [Open](https://stitch.google.com/projects/17153754672098888646/screens/ed53b321004d4b78ba1512f206943440) | — |
| error | — | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features cards --force
```