# statements — error state

| Field | Value |
|-------|-------|
| Feature | statements |
| State | error |
| Screen ID | 40afa7418f034735bd6a267bd5f5ef70 |
| Project ID | 5458150709735075451 |
| Design System ID | 8085591672064527850 |
| Generated At | 2026-07-01T11:15:41.470Z |
| HTML Downloaded | Yes |
| PNG Downloaded | Yes |
| Figma Export | — |
| Stitch Screen | [View](https://stitch.google.com/projects/5458150709735075451/screens/40afa7418f034735bd6a267bd5f5ef70) |
| Attempts | 1 |

## Files

- `code.html` — Stitch-generated HTML mockup
- `screen.png` — Screenshot of the generated screen

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features statements --force
```