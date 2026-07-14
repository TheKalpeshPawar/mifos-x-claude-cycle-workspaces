# statement-detail — error state

| Field | Value |
|-------|-------|
| Feature | statement-detail |
| State | error |
| Screen ID | cccdb01ad3fd41579aab6efb055876ab |
| Project ID | 5458150709735075451 |
| Design System ID | 8085591672064527850 |
| Generated At | 2026-07-01T10:59:44.585Z |
| HTML Downloaded | Yes |
| PNG Downloaded | Yes |
| Figma Export | — |
| Stitch Screen | [View](https://stitch.google.com/projects/5458150709735075451/screens/cccdb01ad3fd41579aab6efb055876ab) |
| Attempts | 1 |

## Files

- `code.html` — Stitch-generated HTML mockup
- `screen.png` — Screenshot of the generated screen

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features statement-detail --force
```