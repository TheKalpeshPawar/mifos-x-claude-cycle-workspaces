# FIGMA_LINKS.md — consent-callback

<!-- schema: v3.2 | generated: 2026-07-01T10:51:08.363Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [5458150709735075451](https://stitch.google.com/projects/5458150709735075451) |
| Design System ID | 8085591672064527850 |
| Generated | 2026-07-01T10:51:03.658Z |
| Success | 6/6 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | 345585a46b2c4e58b707e635b709e33c | 01-consent-callback-loading | PNG ✅ | HTML ✅ | ✅ generated |
| content | 26d7a9b3217848f8bd9f522ddb88ce80 | 02-consent-callback-content | PNG ✅ | HTML ✅ | ✅ generated |
| empty | ebccda17b9474b528ad3b88fe4bb9f4a | 03-consent-callback-empty | PNG ✅ | HTML ✅ | ✅ generated |
| error | 68d14027b2154677a902663b4a48c218 | 04-consent-callback-error | PNG ✅ | HTML ✅ | ✅ generated |
| access_denied | 5fbb78d75e634504981b9222374e5f4c | 05-consent-callback-access_denied | PNG ✅ | HTML ✅ | ✅ generated |
| security_error | 5d1f3143fd84445baa1c9d4d4230309f | 06-consent-callback-security_error | PNG ✅ | HTML ✅ | ✅ generated |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | [Open](https://stitch.google.com/projects/5458150709735075451/screens/345585a46b2c4e58b707e635b709e33c) | — |
| content | [Open](https://stitch.google.com/projects/5458150709735075451/screens/26d7a9b3217848f8bd9f522ddb88ce80) | — |
| empty | [Open](https://stitch.google.com/projects/5458150709735075451/screens/ebccda17b9474b528ad3b88fe4bb9f4a) | — |
| error | [Open](https://stitch.google.com/projects/5458150709735075451/screens/68d14027b2154677a902663b4a48c218) | — |
| access_denied | [Open](https://stitch.google.com/projects/5458150709735075451/screens/5fbb78d75e634504981b9222374e5f4c) | — |
| security_error | [Open](https://stitch.google.com/projects/5458150709735075451/screens/5d1f3143fd84445baa1c9d4d4230309f) | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features consent-callback --force
```