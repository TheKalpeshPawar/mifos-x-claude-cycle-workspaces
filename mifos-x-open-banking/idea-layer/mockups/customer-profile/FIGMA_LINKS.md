# FIGMA_LINKS.md — customer-profile

<!-- schema: v3.2 | generated: 2026-06-02T05:30:06.064Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [17153754672098888646](https://stitch.google.com/projects/17153754672098888646) |
| Design System ID | 2005644667042354169 |
| Generated | 2026-06-02T05:30:06.064Z |
| Success | 0/6 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | — | 01-customer-profile-loading | PNG ❌ | HTML ❌ | ❌ StitchError: Incomplete API response from generate_screen_from_text: expected object at projection path |
| content | — | 02-customer-profile-content | PNG ❌ | HTML ❌ | ❌ StitchError: Tool Call Failed [generate_screen_from_text]: The service is currently unavailable. |
| editing | — | 03-customer-profile-editing | PNG ❌ | HTML ❌ | ❌ StitchError: Tool Call Failed [generate_screen_from_text]: The service is currently unavailable. |
| saving | — | 04-customer-profile-saving | PNG ❌ | HTML ❌ | ❌ StitchError: Tool Call Failed [generate_screen_from_text]: The service is currently unavailable. |
| error | — | 05-customer-profile-error | PNG ❌ | HTML ❌ | ❌ StitchError: Incomplete API response from generate_screen_from_text: expected object at projection path |
| empty | — | 06-customer-profile-empty | PNG ❌ | HTML ❌ | ❌ StitchError: Tool Call Failed [generate_screen_from_text]: The service is currently unavailable. |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | — | — |
| content | — | — |
| editing | — | — |
| saving | — | — |
| error | — | — |
| empty | — | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features customer-profile --force
```