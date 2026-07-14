# product — error state

| Field | Value |
|-------|-------|
| Feature | product |
| State | error |
| Screen ID | ee143ea6785043f08a52ae27467111de |
| Project ID | 5458150709735075451 |
| Design System ID | 8085591672064527850 |
| Generated At | 2026-07-01T10:52:41.628Z |
| HTML Downloaded | Yes |
| PNG Downloaded | Yes |
| Figma Export | — |
| Stitch Screen | [View](https://stitch.google.com/projects/5458150709735075451/screens/ee143ea6785043f08a52ae27467111de) |
| Attempts | 1 |

## Files

- `code.html` — Stitch-generated HTML mockup
- `screen.png` — Screenshot of the generated screen

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features product --force
```