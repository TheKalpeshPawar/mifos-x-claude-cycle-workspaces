# FIGMA_LINKS.md — user-onboarding

<!-- schema: v3.2 | generated: 2026-07-01T11:09:01.392Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [5458150709735075451](https://stitch.google.com/projects/5458150709735075451) |
| Design System ID | 8085591672064527850 |
| Generated | 2026-07-01T11:09:01.392Z |
| Success | 4/4 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| intro | 9940bbaa552f435494d37cca5eb74d3e | 01-user-onboarding-intro | PNG ✅ | HTML ✅ | ✅ generated |
| permissions_overview | 1ee0a9b42567463db7c801c9e0d59ca4 | 02-user-onboarding-permissions_overview | PNG ✅ | HTML ✅ | ✅ generated |
| consent_explainer | 703b057269d84558bd917b9d22feae75 | 03-user-onboarding-consent_explainer | PNG ✅ | HTML ✅ | ✅ generated |
| ob_explainer_open | 1ac09e08637e4934af2b18a3c82cfb2f | 04-user-onboarding-ob_explainer_open | PNG ✅ | HTML ✅ | ✅ generated |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| intro | [Open](https://stitch.google.com/projects/5458150709735075451/screens/9940bbaa552f435494d37cca5eb74d3e) | — |
| permissions_overview | [Open](https://stitch.google.com/projects/5458150709735075451/screens/1ee0a9b42567463db7c801c9e0d59ca4) | — |
| consent_explainer | [Open](https://stitch.google.com/projects/5458150709735075451/screens/703b057269d84558bd917b9d22feae75) | — |
| ob_explainer_open | [Open](https://stitch.google.com/projects/5458150709735075451/screens/1ac09e08637e4934af2b18a3c82cfb2f) | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features user-onboarding --force
```