---
ui_yaml_sha: 5b4e63fd968d1623f04fb68f35f8d1f64c6a5215034b56bce2efabe7cb563790
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 3d7f4b55489427e87257a0ce89adbf58eeff5483f040b815bd72cd4276da0c25

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: fx-rates
state: empty
state_visibility: empty

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# fx-rates — empty state

> Auto-generated from screens/fx-rates/ui.yaml @ SHA 7504059146816f6a
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the empty state of the fx-rates screen for **Mifos X Open Banking**, a Open Banking KMP super-app for consumer retail banking and field officer agent banking in emerging markets.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, error #FFB4AB, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, outline #8F9285, pending #E8A317.

**Component 1 — App Bar** (full width, 56dp tall): Title "Exchange Rates" Outfit Medium 18sp #E3E3D8 centered. Background #12140E. Zero elevation.

**Component 2 — Hero** (centered, top margin 80dp, horizontal padding 48dp): Illustration of currency symbols or globe rendered in #1E201A surface tones on #12140E background. empty_state archetype.

**Component 3 — App Bar** (centered, top margin 24dp, horizontal padding 32dp): Title "Rates unavailable" Outfit SemiBold 22sp #E3E3D8 centered.

**Component 4 — List Row** (centered, top margin 8dp, horizontal padding 48dp): Subtext "Exchange rate data is not available at the moment. Check back shortly." Outfit Regular 14sp #C5C8BA line-height 20sp centered max 25 words.

**Component 5 — Button** (full width minus 64dp insets, top margin 32dp): Filled pill button 48dp tall, 999dp corner radius, background #B2D188, label "Refresh Rates" Outfit SemiBold 16sp #1F3701.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Centered layout on #12140E with generous vertical breathing room. The earth-green #B2D188 on the refresh button communicates that recovery is close, keeping the experience calm and balanced throughout.

## State-specific behavior
- Show an empty-state illustration, a friendly message, and one primary call-to-action button.

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

- [ ] **Per-state shape:** the render shows ONLY this state ("empty"). Do not blend multiple states into one mockup.
- [ ] **Real content:** every text label, image, and data point reflects the content source manifest above — no numbered generic items, no filler text, no dummy text, no empty strings.
- [ ] **Token fidelity:** colors come from the uploaded design system (primary/secondary/surface/etc.) by name; spacing comes from declared scale tokens. No invented hex codes, no invented size literals.
- [ ] **Component vocabulary:** every component in the render maps to a named design-system component (Card, FAB, BottomBar, etc.) — no invented or off-system components.
- [ ] **Archetype honored:** the layout follows the "screen" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

Anchored by the earth-green #B2D188 on the refresh action, the layout stays calm and balanced through the absence of data.

↑↑↑ MOCKUP PROMPT
