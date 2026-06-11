# FIGMA_LINKS.md — change-password

<!-- schema: v3.2 | generated: 2026-06-05T10:29:57.500Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [17153754672098888646](https://stitch.google.com/projects/17153754672098888646) |
| Design System ID | 2005644667042354169 |
| Generated | 2026-06-05T10:29:37.068Z |
| Success | 3/7 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | 8ad85303c292436da8ff106381b12697 | 01-change-password-loading | PNG ✅ | HTML ✅ | ♻ resumed |
| idle | 0d0ab7d15bd64832acb40523e6acfee0 | 02-change-password-idle | PNG ✅ | HTML ✅ | ♻ resumed |
| submitting | — | 03-change-password-submitting | PNG ❌ | HTML ❌ | ❌ StitchError: Tool Call Failed [generate_screen_from_text]: The service is currently unavailable. |
| success | — | 04-change-password-success | PNG ❌ | HTML ❌ | ❌ StitchError: Tool Call Failed [generate_screen_from_text]: The service is currently unavailable. |
| error | — | 05-change-password-error | PNG ❌ | HTML ❌ | ❌ StitchError: Tool Call Failed [generate_screen_from_text]: The service is currently unavailable. |
| content | 262d686301aa4080a0c2e5efe8ffd7ff | 06-change-password-content | PNG ✅ | HTML ✅ | ♻ resumed |
| empty | — | 07-change-password-empty | PNG ❌ | HTML ❌ | ❌ StitchError: Tool Call Failed [generate_screen_from_text]: The service is currently unavailable. |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | [Open](https://stitch.google.com/projects/17153754672098888646/screens/8ad85303c292436da8ff106381b12697) | — |
| idle | [Open](https://stitch.google.com/projects/17153754672098888646/screens/0d0ab7d15bd64832acb40523e6acfee0) | — |
| submitting | — | — |
| success | — | — |
| error | — | — |
| content | [Open](https://stitch.google.com/projects/17153754672098888646/screens/262d686301aa4080a0c2e5efe8ffd7ff) | — |
| empty | — | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features change-password --force
```