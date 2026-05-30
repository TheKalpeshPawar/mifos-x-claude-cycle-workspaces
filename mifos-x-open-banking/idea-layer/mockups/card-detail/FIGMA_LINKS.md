# FIGMA_LINKS.md — card-detail

<!-- schema: v3.2 | generated: 2026-05-30T06:46:14.887Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [17153754672098888646](https://stitch.google.com/projects/17153754672098888646) |
| Design System ID | 2005644667042354169 |
| Generated | 2026-05-30T06:46:14.526Z |
| Success | 5/5 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | ae3df382319d4a09b408a38504bcdfbb | 01-card-detail-loading | PNG ✅ | HTML ✅ | ✅ generated |
| content | a86724d20f3a4b37b33693b4457970fe | 02-card-detail-content | PNG ❌ | HTML ✅ | ✅ generated |
| frozen | d43bd6a8854e48e7abc2650282db2cd9 | 03-card-detail-frozen | PNG ✅ | HTML ❌ | ✅ generated |
| error | b90b3a8328e945cd94e820721cf4217d | 04-card-detail-error | PNG ❌ | HTML ✅ | ✅ generated |
| empty | 1a10e29d6aa14ff4b4d843e9d8360dac | 05-card-detail-empty | PNG ✅ | HTML ✅ | ✅ generated |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | [Open](https://stitch.google.com/projects/17153754672098888646/screens/ae3df382319d4a09b408a38504bcdfbb) | — |
| content | [Open](https://stitch.google.com/projects/17153754672098888646/screens/a86724d20f3a4b37b33693b4457970fe) | — |
| frozen | [Open](https://stitch.google.com/projects/17153754672098888646/screens/d43bd6a8854e48e7abc2650282db2cd9) | — |
| error | [Open](https://stitch.google.com/projects/17153754672098888646/screens/b90b3a8328e945cd94e820721cf4217d) | — |
| empty | [Open](https://stitch.google.com/projects/17153754672098888646/screens/1a10e29d6aa14ff4b4d843e9d8360dac) | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features card-detail --force
```