# FIGMA_LINKS.md — cards

<!-- schema: v3.2 | generated: 2026-06-02T06:05:10.002Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [17153754672098888646](https://stitch.google.com/projects/17153754672098888646) |
| Design System ID | 2005644667042354169 |
| Generated | 2026-06-02T06:05:10.001Z |
| Success | 1/4 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | 34bee5f13b5a4dfbbee2532f4dc017ad | 01-cards-loading | PNG ✅ | HTML ✅ | ♻ resumed |
| content | — | 02-cards-content | PNG ❌ | HTML ❌ | ❌ StitchError: Streamable HTTP error: Error POSTing to endpoint: {"id":1,"jsonrpc":"2.0","result":{"content":[{"text":"Stitch API has not been used in project composed-field-479309-e0 before or it is disabled. Enable it by visiting https://console.developers.google.com/apis/api/stitch.googleapis.com/overview?project=composed-field-479309-e0 then retry. If you enabled this API recently, wait a few minutes for the action to propagate to our systems and retry.","type":"text"}],"isError":true}} |
| empty | — | 03-cards-empty | PNG ❌ | HTML ❌ | ❌ StitchError: Streamable HTTP error: Error POSTing to endpoint: {"id":2,"jsonrpc":"2.0","result":{"content":[{"text":"Stitch API has not been used in project composed-field-479309-e0 before or it is disabled. Enable it by visiting https://console.developers.google.com/apis/api/stitch.googleapis.com/overview?project=composed-field-479309-e0 then retry. If you enabled this API recently, wait a few minutes for the action to propagate to our systems and retry.","type":"text"}],"isError":true}} |
| error | — | 04-cards-error | PNG ❌ | HTML ❌ | ❌ StitchError: Streamable HTTP error: Error POSTing to endpoint: {"id":3,"jsonrpc":"2.0","result":{"content":[{"text":"Stitch API has not been used in project composed-field-479309-e0 before or it is disabled. Enable it by visiting https://console.developers.google.com/apis/api/stitch.googleapis.com/overview?project=composed-field-479309-e0 then retry. If you enabled this API recently, wait a few minutes for the action to propagate to our systems and retry.","type":"text"}],"isError":true}} |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | [Open](https://stitch.google.com/projects/17153754672098888646/screens/34bee5f13b5a4dfbbee2532f4dc017ad) | — |
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
  --workspace mifos-x/mifos-x-open-banking --features cards --force
```