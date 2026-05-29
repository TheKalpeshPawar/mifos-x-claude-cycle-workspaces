# FIGMA_LINKS.md — send-money-confirm

<!-- schema: v3.2 | generated: 2026-05-29T17:13:17.693Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [17153754672098888646](https://stitch.google.com/projects/17153754672098888646) |
| Design System ID | 2005644667042354169 |
| Generated | 2026-05-29T17:13:17.693Z |
| Success | 0/7 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | — | 01-send-money-confirm-loading | PNG ❌ | HTML ❌ | ❌ STN gate failure pre-API: STN2: prompt is 4106 chars (cap 4000) — apply the shrink ladder or split the screen |
| review | — | 02-send-money-confirm-review | PNG ❌ | HTML ❌ | ❌ StitchError: Tool Call Failed [generate_screen_from_text]: Resource has been exhausted (e.g. check quota). |
| submitting | — | 03-send-money-confirm-submitting | PNG ❌ | HTML ❌ | ❌ StitchError: Tool Call Failed [generate_screen_from_text]: Resource has been exhausted (e.g. check quota). |
| success | — | 04-send-money-confirm-success | PNG ❌ | HTML ❌ | ❌ StitchError: Tool Call Failed [generate_screen_from_text]: Resource has been exhausted (e.g. check quota). |
| content | — | 05-send-money-confirm-content | PNG ❌ | HTML ❌ | ❌ StitchError: Tool Call Failed [generate_screen_from_text]: Resource has been exhausted (e.g. check quota). |
| empty | — | 06-send-money-confirm-empty | PNG ❌ | HTML ❌ | ❌ STN gate failure pre-API: STN2: prompt is 4268 chars (cap 4000) — apply the shrink ladder or split the screen |
| error | — | 07-send-money-confirm-error | PNG ❌ | HTML ❌ | ❌ STN gate failure pre-API: STN2: prompt is 4268 chars (cap 4000) — apply the shrink ladder or split the screen |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | — | — |
| review | — | — |
| submitting | — | — |
| success | — | — |
| content | — | — |
| empty | — | — |
| error | — | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features send-money-confirm --force
```