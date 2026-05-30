# FIGMA_LINKS.md — accounts

<!-- schema: v3.2 | generated: 2026-05-30T06:58:10.510Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [17153754672098888646](https://stitch.google.com/projects/17153754672098888646) |
| Design System ID | 2005644667042354169 |
| Generated | 2026-05-30T06:58:10.509Z |
| Success | 2/4 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | b778b6fd6daf4ccc8890f24e8cb1719f | 01-accounts-loading | PNG ✅ | HTML ✅ | ♻ resumed |
| content | — | 02-accounts-content | PNG ❌ | HTML ❌ | ❌ StitchError: Tool Call Failed [generate_screen_from_text]: Resource has been exhausted (e.g. check quota). |
| empty | 07f3f4812ea4480a85f2e865466ea7ea | 03-accounts-empty | PNG ✅ | HTML ✅ | ♻ resumed |
| error | — | 04-accounts-error | PNG ❌ | HTML ❌ | ❌ StitchError: Tool Call Failed [generate_screen_from_text]: Resource has been exhausted (e.g. check quota). |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | [Open](https://stitch.google.com/projects/17153754672098888646/screens/b778b6fd6daf4ccc8890f24e8cb1719f) | — |
| content | — | — |
| empty | [Open](https://stitch.google.com/projects/17153754672098888646/screens/07f3f4812ea4480a85f2e865466ea7ea) | — |
| error | — | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features accounts --force
```