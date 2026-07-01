---
ui_yaml_sha: 3747e8c19a3ae10585439a8bc5107c3be3bd474302e2738ad1672d41544a35e8
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 59778d6f1ab191b6c24797591f5396558e997d533d896d12bc244d445d44943d

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: statements
state: loading
state_visibility: loading

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# statements — loading state

> Auto-generated from screens/statements/ui.yaml @ SHA 8f19c7fab6d83da0
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the statements screen for **HSBC Open Banking**, a UK AISP reference app fetching OBReadStatement2 statement period data from HSBC, within the Trust Blue minimalist Material 3 dark system on a 393x852dp Pixel 5.

Palette: primary #95CDF7, onPrimary #00344E, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, surfaceContainerHigh #262A2E, surfaceContainerHighest #313539, onSurfaceVariant #C1C7CE, outline #8B9198, outlineVariant #41474D

**Component 1 - Top App Bar** (full width, 64dp, bg #101417): back-arrow icon #C1C7CE left; shimmer bar 100x18dp at title position in #262A2E with #313539 sweep; no real text.

**Component 2 - List** (full width minus 32dp insets, bg #101417): 6 skeleton rows stacked, each 72dp tall, separated by 1dp static #41474D dividers; skeleton_screen archetype. Each row: shimmer bar 120x16dp left #262A2E for month label; shimmer bar 160x14dp below-left #262A2E for date range; static chevron-right placeholder 20dp #41474D right; bars animate with synchronized left-to-right #313539 sweep.

**Component 3 - Bottom Navigation Bar** (full width, 80dp, bg #1C2024): items "Home", "Accounts", "Statements", "More" in static #C1C7CE; navigation is not shimmered.

Do not render any real month labels, date range strings, or the Chip Row filter; all text positions hold only shimmer bars. Do not add a top Chip Row in the loading state; the chip appears only after content has loaded. Do not collapse row height during loading; skeleton rows maintain the 72dp content-state footprint. Do not show an Empty State or Error State component in the loading view.

Patient skeleton. Layout mirrors content geometry. No period data revealed. Tone: minimal, #95CDF7 restrained.

↑↑↑ MOCKUP PROMPT

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
- [ ] **Archetype honored:** the layout follows the "screen" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
