---
ui_yaml_sha: b89d839e6c9e3be9d2a9ef40cf53bd6b62a21124885037343b404ee39dd8d76d
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 5fb79b99aeb3ce0764bce161561fba90cf8634b3fc56a7c8969b258e46bb1d9e

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: home
state: loading
state_visibility: loading

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# home — loading state

> Auto-generated from screens/home/ui.yaml @ SHA 041f8010d0411280
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the home screen for **Mifos X Open Banking**, a Open Banking KMP super-app for consumer retail banking and field officer agent banking in emerging markets.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, error #FFB4AB, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, outline #8F9285, pending #E8A317.

**Component 1 — App Bar Shimmer** (56dp tall, full width): Two stacked shimmer rectangles left-aligned with 16dp padding, 200dp x 20dp and 140dp x 14dp, top margin 8dp between them. Background #12140E. Shimmer base #1E201A, highlight #282A24, 1200ms sweep. skeleton_screen archetype.

**Component 2 — Card Shimmer** (full width minus 32dp insets, top margin 16dp, 16dp corner radius, 140dp tall, background #354E16 at 50% opacity): Account card shimmer. Two text-line shimmers 120dp x 14dp and 80dp x 12dp stacked top-left. Balance shimmer 180dp x 32dp below. Three chip shimmers each 96dp x 32dp in a row with 8dp gap.

**Component 3 — Card Shimmer** (full width minus 32dp insets, top margin 12dp, 12dp corner radius, 40dp tall, background #1E201A): Balance chip shimmer, full-width rectangle.

**Component 4 — List Row Shimmer** (full width minus 32dp insets, top margin 24dp): Header row with 180dp x 16dp shimmer left and 60dp x 14dp right. Three transaction row shimmers each 64dp tall. Each row: 40dp x 40dp circular shimmer left, two text shimmers 160dp x 14dp and 100dp x 12dp center, 50dp x 14dp shimmer right.

**Component 5 — Grid Shimmer** (full width minus 32dp insets, top margin 24dp): Header shimmer 80dp x 16dp. Two-column grid with 3 card shimmers each 80dp tall 12dp corner radius background #1E201A.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Full scrollable layout on pure #12140E. Shimmer placeholders at surface_container #1E201A with #282A24 highlight create a calm, structured loading atmosphere matching the banking-grade trust aesthetic.

## State-specific behavior
- Show shimmer/skeleton loaders matching the content layout block-for-block — no real text, no images.

## Content source manifest
- (no demo collections bound for this state)

## Components (vocabulary used in this prompt)
- (no named components extracted — see composition)

## Shell (app-shell resolved for this state)
- App-shell rules are defined per project; per-screen overrides are merged in.
- Render MUST keep nav/bar elements consistent with the resolved shell — present or absent, never partial.

## Tokens (design-tokens roles consumed)
- Colors: primary / secondary / surface / on-surface / on-surface-variant / error (M3 standard roles).
- Typography: body-large / title-large (M3 standard roles).
- Spacing: gap.sm / gap.md / gap.lg.
- ALL token references are by name from the uploaded design system — no hex literals, no inline size values.

## Self-Validation Checklist (MANDATORY)

Before returning the rendered mockup, verify ALL of these are true. If any fails, FIX the output and re-render.

- [ ] **Per-state shape:** the render shows ONLY this state ("loading"). Do not blend multiple states into one mockup.
- [ ] **Real content:** every text label, image, and data point reflects the content source manifest above — no numbered generic items, no filler text, no dummy text, no empty strings.
- [ ] **Token fidelity:** colors come from the uploaded design system (primary/secondary/surface/etc.) by name; spacing comes from declared scale tokens. No invented hex codes, no invented size literals.
- [ ] **Component vocabulary:** every component in the render maps to a named design-system component (Card, FAB, BottomBar, etc.) — no invented or off-system components.
- [ ] **Archetype honored:** the layout follows the "dashboard" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

Anchored by the shimmer accent #B2D188 awaiting reveal, the loading skeleton stays calm and balanced throughout retrieval.

↑↑↑ MOCKUP PROMPT
