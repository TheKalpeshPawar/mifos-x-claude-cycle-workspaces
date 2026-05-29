# FIGMA_LINKS.md — agent-registration

<!-- schema: v3.2 | generated: 2026-05-29T17:13:06.927Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [17153754672098888646](https://stitch.google.com/projects/17153754672098888646) |
| Design System ID | 2005644667042354169 |
| Generated | 2026-05-29T17:13:01.964Z |
| Success | 0/9 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | — | 01-agent-registration-loading | PNG ❌ | HTML ❌ | ❌ STN gate failure pre-API: STN2: prompt is 5410 chars (cap 4000) — apply the shrink ladder or split the screen |
| idle | — | 02-agent-registration-idle | PNG ❌ | HTML ❌ | ❌ STN gate failure pre-API: STN2: prompt is 4929 chars (cap 4000) — apply the shrink ladder or split the screen |
| submitting | — | 03-agent-registration-submitting | PNG ❌ | HTML ❌ | ❌ STN gate failure pre-API: STN2: prompt is 4935 chars (cap 4000) — apply the shrink ladder or split the screen |
| validation_error | — | 04-agent-registration-validation_error | PNG ❌ | HTML ❌ | ❌ STN gate failure pre-API: STN2: prompt is 4941 chars (cap 4000) — apply the shrink ladder or split the screen |
| pending_approval | — | 05-agent-registration-pending_approval | PNG ❌ | HTML ❌ | ❌ STN gate failure pre-API: STN2: prompt is 4941 chars (cap 4000) — apply the shrink ladder or split the screen |
| confirmed | — | 06-agent-registration-confirmed | PNG ❌ | HTML ❌ | ❌ STN gate failure pre-API: STN2: prompt is 4934 chars (cap 4000) — apply the shrink ladder or split the screen |
| content | — | 07-agent-registration-content | PNG ❌ | HTML ❌ | ❌ STN gate failure pre-API: STN2: prompt is 4932 chars (cap 4000) — apply the shrink ladder or split the screen |
| empty | — | 08-agent-registration-empty | PNG ❌ | HTML ❌ | ❌ STN gate failure pre-API: STN2: prompt is 5644 chars (cap 4000) — apply the shrink ladder or split the screen |
| error | — | 09-agent-registration-error | PNG ❌ | HTML ❌ | ❌ STN gate failure pre-API: STN2: prompt is 5644 chars (cap 4000) — apply the shrink ladder or split the screen |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | — | — |
| idle | — | — |
| submitting | — | — |
| validation_error | — | — |
| pending_approval | — | — |
| confirmed | — | — |
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
  --workspace mifos-x/mifos-x-open-banking --features agent-registration --force
```