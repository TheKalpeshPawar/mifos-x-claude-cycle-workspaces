# FIGMA_LINKS.md — kyc-review

<!-- schema: v3.2 | generated: 2026-05-31T05:30:22.737Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [17153754672098888646](https://stitch.google.com/projects/17153754672098888646) |
| Design System ID | 2005644667042354169 |
| Generated | 2026-05-31T05:30:22.728Z |
| Success | 1/3 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| content | ccdc36c54b064bef80a910352ebb0fcb | 01-kyc-review-content | PNG ✅ | HTML ✅ | ✅ generated |
| empty | — | 02-kyc-review-empty | PNG ❌ | HTML ❌ | ❌ StitchError: Tool Call Failed [generate_screen_from_text]: The service is currently unavailable. |
| error | — | 03-kyc-review-error | PNG ❌ | HTML ❌ | ❌ StitchError: Tool Call Failed [generate_screen_from_text]: The service is currently unavailable. |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| content | [Open](https://stitch.google.com/projects/17153754672098888646/screens/ccdc36c54b064bef80a910352ebb0fcb) | — |
| empty | — | — |
| error | — | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features kyc-review --force
```