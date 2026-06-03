# FIGMA_LINKS.md — customer-onboarding

<!-- schema: v3.2 | generated: 2026-06-02T05:25:52.504Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [17153754672098888646](https://stitch.google.com/projects/17153754672098888646) |
| Design System ID | 2005644667042354169 |
| Generated | 2026-06-02T05:25:52.503Z |
| Success | 0/9 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| step_1 | — | 01-customer-onboarding-step_1 | PNG ❌ | HTML ❌ | ❌ StitchError: Tool Call Failed [generate_screen_from_text]: The service is currently unavailable. |
| step_2 | — | 02-customer-onboarding-step_2 | PNG ❌ | HTML ❌ | ❌ StitchError: Tool Call Failed [generate_screen_from_text]: The service is currently unavailable. |
| step_3 | — | 03-customer-onboarding-step_3 | PNG ❌ | HTML ❌ | ❌ StitchError: Tool Call Failed [generate_screen_from_text]: The service is currently unavailable. |
| step_4 | — | 04-customer-onboarding-step_4 | PNG ❌ | HTML ❌ | ❌ StitchError: Tool Call Failed [generate_screen_from_text]: The service is currently unavailable. |
| loading | — | 05-customer-onboarding-loading | PNG ❌ | HTML ❌ | ❌ StitchError: Tool Call Failed [generate_screen_from_text]: The service is currently unavailable. |
| submitted | — | 06-customer-onboarding-submitted | PNG ❌ | HTML ❌ | ❌ StitchError: Tool Call Failed [generate_screen_from_text]: The service is currently unavailable. |
| error | — | 07-customer-onboarding-error | PNG ❌ | HTML ❌ | ❌ StitchError: Incomplete API response from generate_screen_from_text: expected object at projection path |
| content | — | 08-customer-onboarding-content | PNG ❌ | HTML ❌ | ❌ StitchError: Tool Call Failed [generate_screen_from_text]: The service is currently unavailable. |
| empty | — | 09-customer-onboarding-empty | PNG ❌ | HTML ❌ | ❌ StitchError: Incomplete API response from generate_screen_from_text: expected object at projection path |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| step_1 | — | — |
| step_2 | — | — |
| step_3 | — | — |
| step_4 | — | — |
| loading | — | — |
| submitted | — | — |
| error | — | — |
| content | — | — |
| empty | — | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features customer-onboarding --force
```