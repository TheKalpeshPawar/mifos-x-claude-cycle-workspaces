# FIGMA_LINKS.md — consent-detail

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
| loading | a85b205cdea24f4da7f4f4bde08fd17d | 01-consent-detail-loading | PNG ✅ | HTML ✅ | ✅ generated |
| content | 66e75c5547874a14a17fc3c60cd22e2e | 02-consent-detail-content | PNG ❌ | HTML ✅ | ✅ generated |
| revoke_confirm | 246ec7dfe5d448898a6356dbdc10dc26 | 03-consent-detail-revoke_confirm | PNG ✅ | HTML ✅ | ✅ generated |
| revoking | 2e595e0b07a445c9b6727b9cd29f08f6 | 04-consent-detail-revoking | PNG ✅ | HTML ✅ | ✅ generated |
| error | eba73db1613a45809f199c3e79a0123e | 05-consent-detail-error | PNG ✅ | HTML ✅ | ✅ generated |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | [Open](https://stitch.google.com/projects/5458150709735075451/screens/a85b205cdea24f4da7f4f4bde08fd17d) | — |
| content | [Open](https://stitch.google.com/projects/5458150709735075451/screens/66e75c5547874a14a17fc3c60cd22e2e) | — |
| revoke_confirm | [Open](https://stitch.google.com/projects/5458150709735075451/screens/246ec7dfe5d448898a6356dbdc10dc26) | — |
| revoking | [Open](https://stitch.google.com/projects/5458150709735075451/screens/2e595e0b07a445c9b6727b9cd29f08f6) | — |
| error | [Open](https://stitch.google.com/projects/5458150709735075451/screens/eba73db1613a45809f199c3e79a0123e) | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features consent-detail --force
```