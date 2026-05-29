# application-detail — empty state

| Field | Value |
|-------|-------|
| Feature | application-detail |
| State | empty |
| Screen ID | f0bc75cc0156458db99d4d5124fcced2 |
| Project ID | 17153754672098888646 |
| Design System ID | 2005644667042354169 |
| Generated At | 2026-05-29T16:56:53.584Z |
| HTML Downloaded | No |
| PNG Downloaded | Yes |
| Figma Export | — |
| Stitch Screen | [View](https://stitch.google.com/projects/17153754672098888646/screens/f0bc75cc0156458db99d4d5124fcced2) |
| Attempts | 1 |

## Files

- `code.html` — Stitch-generated HTML mockup
- `screen.png` — Screenshot of the generated screen

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-open-banking --features application-detail --force
```