---
ui_yaml_sha: c2e476dbefd7802fb6020d1e81e73e172adfc88161c6aa03ff0f02d312619ff7
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 4334bc3f24e9982977f16de6bd0efdc34076f4ea7709913b22f63ccdbbbbe296

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: statement-detail
state: loading
state_visibility: loading

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# statement-detail — loading state

> Auto-generated from screens/statement-detail/ui.yaml @ SHA d5ef7affea8a27c8
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the statement-detail screen for **HSBC Open Banking**, a UK AISP reference app fetching a June 2026 OBReadStatement2 record from HSBC, within the Trust Blue minimalist Material 3 dark system on a 393x852dp Pixel 5.

Palette: primary #95CDF7, onPrimary #00344E, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, surfaceContainerHigh #262A2E, surfaceContainerHighest #313539, onSurfaceVariant #C1C7CE, outline #8B9198, primaryContainer #004B6F

**Component 1 - Top App Bar** (full width, 64dp, bg #101417): back-arrow icon #C1C7CE left; shimmer bar 160x18dp at title position in #262A2E with #313539 sweep; no real text. This is the skeleton_screen archetype.

**Component 2 - Card** (full width minus 32dp, 80dp, r=12dp, bg #1C2024): shimmer bar 180x14dp left #262A2E for date range placeholder; shimmer badge 80x20dp right #262A2E for type placeholder; both bars animate with #313539 sweep.

**Component 3 - Stat Block** (full width minus 32dp, 112dp, r=12dp, bg #1C2024): 2-column layout with 1dp #41474D center divider; left cell shimmer bars 100x12dp label position #262A2E, 120x20dp amount position #262A2E; right cell identical shimmer bars; synchronized sweep.

**Component 4 - List** (full width minus 32dp, bg #101417): shimmer bar 60x12dp at section label position #262A2E; 2 rows each 56dp: each row left shimmer bar 140x16dp and right shimmer bar 80x16dp; 1dp #41474D static dividers between rows.

**Component 5 - List** (full width minus 32dp, bg #101417): shimmer bar 40x12dp section label; 1 row 56dp with left shimmer 120x16dp and right shimmer 60x16dp.

**Component 6 - List** (full width minus 32dp, bg #101417): shimmer bar 50x12dp section label; 1 row 56dp identical shimmer pattern.

**Component 7 - List** (full width minus 32dp, bg #101417): shimmer bar 90x12dp section label #262A2E; 3 rows 64dp each: each row left shimmer 160x16dp, stacked right shimmers 80x14dp top and 80x14dp bottom; all #262A2E with #313539 sweep; 1dp #41474D static dividers.

**Component 8 - Button** (full width minus 32dp, 52dp, r=12dp, bg #262A2E): shimmer bar 200x16dp centered; full #313539 sweep; no text visible.

**Component 9 - Bottom Navigation Bar** (full width, 80dp, bg #1C2024): items "Home", "Accounts", "Statements", "More" static #C1C7CE; navigation is not shimmered.

Do not reveal any real dates, balances, transaction descriptions, or amounts; all data positions hold only shimmer bars. Do not use a circular spinner overlay on top of the skeleton; shimmer sweep is the exclusive loading indicator. Do not collapse any section List height; all skeleton sections maintain the content-state dimensions exactly. Do not show an Empty State or Error State component in the loading view.

Faithful geometry. Every section placeholder visible. No data revealed prematurely. Tone: balanced, #95CDF7 minimal.

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
