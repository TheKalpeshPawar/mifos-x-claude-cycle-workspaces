# transactions — empty state

| Field | Value |
|-------|-------|
| Feature | transactions |
| State | empty |
| Screen ID | 7a492d82b2ab40db830268c3612d752e |
| Project ID | 5458150709735075451 |
| Design System ID | 8085591672064527850 |
| Generated At | 2026-07-01T10:59:44.585Z |
| HTML Downloaded | Yes |
| PNG Downloaded | Yes |
| Figma Export | — |
| Stitch Screen | [View](https://stitch.google.com/projects/5458150709735075451/screens/7a492d82b2ab40db830268c3612d752e) |
| Attempts | 2 |

## Files

- `code.html` — Stitch-generated HTML mockup
- `screen.png` — Screenshot of the generated screen

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features transactions --force
```