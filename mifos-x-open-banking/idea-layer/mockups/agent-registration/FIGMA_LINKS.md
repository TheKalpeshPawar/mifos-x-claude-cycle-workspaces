# FIGMA_LINKS.md — agent-registration

<!-- schema: v3.2 | generated: 2026-05-31T03:34:29.047Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [17153754672098888646](https://stitch.google.com/projects/17153754672098888646) |
| Design System ID | 2005644667042354169 |
| Generated | 2026-05-31T03:34:11.045Z |
| Success | 9/9 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | 596eb559962949a998174ad727658dfd | 01-agent-registration-loading | PNG ✅ | HTML ✅ | ✅ generated |
| idle | 90a899926c4a4da6b9e4dbe6d3db78bd | 02-agent-registration-idle | PNG ✅ | HTML ✅ | ✅ generated |
| submitting | a2e5fb5fcd9146de99552f0c71339cc2 | 03-agent-registration-submitting | PNG ✅ | HTML ✅ | ✅ generated |
| validation_error | ea26fc38d3224b1c874d3f095813f863 | 04-agent-registration-validation_error | PNG ✅ | HTML ✅ | ✅ generated |
| pending_approval | 7af3ea2b022844b389622f9b16283f2e | 05-agent-registration-pending_approval | PNG ✅ | HTML ✅ | ✅ generated |
| confirmed | 2016318c6dcc4fd98923065c3427fb0a | 06-agent-registration-confirmed | PNG ✅ | HTML ✅ | ✅ generated |
| content | 71711e24f8a6487eaa87b20f40943de2 | 07-agent-registration-content | PNG ✅ | HTML ✅ | ✅ generated |
| empty | f8e4a084e5cc4dd796893ae5eddd4b4a | 08-agent-registration-empty | PNG ✅ | HTML ❌ | ✅ generated |
| error | c5353defe30649748f058485725e8675 | 09-agent-registration-error | PNG ✅ | HTML ❌ | ✅ generated |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | [Open](https://stitch.google.com/projects/17153754672098888646/screens/596eb559962949a998174ad727658dfd) | — |
| idle | [Open](https://stitch.google.com/projects/17153754672098888646/screens/90a899926c4a4da6b9e4dbe6d3db78bd) | — |
| submitting | [Open](https://stitch.google.com/projects/17153754672098888646/screens/a2e5fb5fcd9146de99552f0c71339cc2) | — |
| validation_error | [Open](https://stitch.google.com/projects/17153754672098888646/screens/ea26fc38d3224b1c874d3f095813f863) | — |
| pending_approval | [Open](https://stitch.google.com/projects/17153754672098888646/screens/7af3ea2b022844b389622f9b16283f2e) | — |
| confirmed | [Open](https://stitch.google.com/projects/17153754672098888646/screens/2016318c6dcc4fd98923065c3427fb0a) | — |
| content | [Open](https://stitch.google.com/projects/17153754672098888646/screens/71711e24f8a6487eaa87b20f40943de2) | — |
| empty | [Open](https://stitch.google.com/projects/17153754672098888646/screens/f8e4a084e5cc4dd796893ae5eddd4b4a) | — |
| error | [Open](https://stitch.google.com/projects/17153754672098888646/screens/c5353defe30649748f058485725e8675) | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features agent-registration --force
```