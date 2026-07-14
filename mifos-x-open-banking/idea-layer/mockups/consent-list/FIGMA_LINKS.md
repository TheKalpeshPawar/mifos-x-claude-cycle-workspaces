# FIGMA_LINKS.md — consent-list

<!-- schema: v3.2 | generated: 2026-07-01T10:52:41.600Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [5458150709735075451](https://stitch.google.com/projects/5458150709735075451) |
| Design System ID | 8085591672064527850 |
| Generated | 2026-07-01T10:52:41.600Z |
| Success | 5/5 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | 663ec9c2afb74aaf9ad409d3ec5a183e | 01-consent-list-loading | PNG ✅ | HTML ✅ | ✅ generated |
| content | 67532d7346dc4aebbd36c10fabd5a229 | 02-consent-list-content | PNG ❌ | HTML ✅ | ✅ generated |
| empty | eab0f4217d9243c49a78c0a2f7938f85 | 03-consent-list-empty | PNG ✅ | HTML ✅ | ✅ generated |
| error | 5679dc942beb4db4826e45d9eaf421c3 | 04-consent-list-error | PNG ✅ | HTML ✅ | ✅ generated |
| error_auth | a4966d6920de4023a4b0a49b3b1cc75f | 05-consent-list-error_auth | PNG ✅ | HTML ✅ | ✅ generated |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | [Open](https://stitch.google.com/projects/5458150709735075451/screens/663ec9c2afb74aaf9ad409d3ec5a183e) | — |
| content | [Open](https://stitch.google.com/projects/5458150709735075451/screens/67532d7346dc4aebbd36c10fabd5a229) | — |
| empty | [Open](https://stitch.google.com/projects/5458150709735075451/screens/eab0f4217d9243c49a78c0a2f7938f85) | — |
| error | [Open](https://stitch.google.com/projects/5458150709735075451/screens/5679dc942beb4db4826e45d9eaf421c3) | — |
| error_auth | [Open](https://stitch.google.com/projects/5458150709735075451/screens/a4966d6920de4023a4b0a49b3b1cc75f) | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features consent-list --force
```