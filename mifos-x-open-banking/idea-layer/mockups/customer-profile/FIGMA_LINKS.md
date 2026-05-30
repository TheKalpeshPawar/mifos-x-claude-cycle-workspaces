# FIGMA_LINKS.md — customer-profile

<!-- schema: v3.2 | generated: 2026-05-30T06:58:14.870Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [17153754672098888646](https://stitch.google.com/projects/17153754672098888646) |
| Design System ID | 2005644667042354169 |
| Generated | 2026-05-30T06:58:13.713Z |
| Success | 5/6 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | b209b12c97af492a93dda8b63555fb49 | 01-customer-profile-loading | PNG ✅ | HTML ✅ | ♻ resumed |
| content | 8acc640713ef49838aadae41562abec1 | 02-customer-profile-content | PNG ✅ | HTML ✅ | ♻ resumed |
| editing | c33f18e268f24cc393f1968334fe8220 | 03-customer-profile-editing | PNG ✅ | HTML ✅ | ♻ resumed |
| saving | b838d1cc1cf44518b258c3595abbbf19 | 04-customer-profile-saving | PNG ✅ | HTML ✅ | ♻ resumed |
| error | — | 05-customer-profile-error | PNG ❌ | HTML ❌ | ❌ StitchError: Tool Call Failed [generate_screen_from_text]: Resource has been exhausted (e.g. check quota). |
| empty | b47361f9c6294ce98e1999dc5cdbd706 | 06-customer-profile-empty | PNG ✅ | HTML ✅ | ♻ resumed |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | [Open](https://stitch.google.com/projects/17153754672098888646/screens/b209b12c97af492a93dda8b63555fb49) | — |
| content | [Open](https://stitch.google.com/projects/17153754672098888646/screens/8acc640713ef49838aadae41562abec1) | — |
| editing | [Open](https://stitch.google.com/projects/17153754672098888646/screens/c33f18e268f24cc393f1968334fe8220) | — |
| saving | [Open](https://stitch.google.com/projects/17153754672098888646/screens/b838d1cc1cf44518b258c3595abbbf19) | — |
| error | — | — |
| empty | [Open](https://stitch.google.com/projects/17153754672098888646/screens/b47361f9c6294ce98e1999dc5cdbd706) | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features customer-profile --force
```