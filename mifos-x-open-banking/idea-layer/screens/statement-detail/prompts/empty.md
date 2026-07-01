---
ui_yaml_sha: c2e476dbefd7802fb6020d1e81e73e172adfc88161c6aa03ff0f02d312619ff7
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 9ae190108ef337d536970acf6382d58ae9501bf3515e112a6d82fb245b55b9ca

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: statement-detail
state: empty
state_visibility: empty

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# statement-detail — empty state

> Auto-generated from screens/statement-detail/ui.yaml @ SHA 11caa85f84fbf9f9
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the empty state of the statement-detail screen for **HSBC Open Banking**, a UK AISP reference app rendering a June 2026 OBReadStatement2 record that contains no transactions, within the Trust Blue minimalist Material 3 dark system on a 393x852dp Pixel 5.

Palette: primary #95CDF7, onPrimary #00344E, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, error #FFB4AB, onSurfaceVariant #C1C7CE, outline #8B9198, primaryContainer #004B6F, secondary #B7C9D9

**Component 1 - Top App Bar** (full width, 64dp, bg #101417): back-arrow icon 24dp #95CDF7 left; title Outfit medium 22sp "June 2026 Statement" #E0E3E8.

**Component 2 - Card** (full width minus 32dp, 80dp, r=12dp, bg #1C2024): Outfit regular 14sp "01 Jun 2026 - 30 Jun 2026" #C1C7CE left; badge "RegularPeriodic" 12sp bg #004B6F text #C9E6FF r=full right.

**Component 3 - Stat Block** (full width minus 32dp, 112dp, r=12dp, bg #1C2024): 2-column grid with 1dp #41474D center divider; left "Opening Balance" 12sp #C1C7CE, monospaced bold 18sp "GBP 5,432.18" #95CDF7; right "Closing Balance" 12sp #C1C7CE, monospaced bold 18sp "GBP 4,901.47" #95CDF7.

**Component 4 - Empty State** (full width minus 32dp, vertically centered below Stat Block, centered, generous vertical breathing room): receipt-long icon 48dp #C1C7CE centered; Outfit medium 16sp "No transactions in this period" #E0E3E8 below icon, 12dp gap; Outfit regular 14sp "This statement period recorded no debit or credit transactions on this HSBC account." #C1C7CE centered, 2-line max. This is the empty_state archetype.

**Component 5 - Button** (full width minus 32dp, 52dp, r=12dp, bg #004B6F, label Outfit medium 16sp "Download PDF statement" #C9E6FF, download icon 20dp #95CDF7 left): 24dp below Empty State.

**Component 6 - Bottom Navigation Bar** (full width, 80dp, bg #1C2024): items "Home", "Accounts", "Statements", "More"; "Statements" filled icon #95CDF7; inactive #C1C7CE.

Do not hide the Card header or Stat Block in the empty state; the period dates and balances are valid data even when no transactions are present. Do not remove the download Button; the PDF statement document exists regardless of zero transactions. Do not apply error color #FFB4AB to the empty transactions icon or message; this is informational, not a failure. Do not add a "Transactions" section label above the Empty State component; it stands directly below the Stat Block.

Statement exists, transactions absent. Financial clarity maintained regardless. Tone: calm, #95CDF7 minimal.

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

- [ ] **Per-state shape:** the render shows ONLY this state ("empty"). Do not blend multiple states into one mockup.
- [ ] **Real content:** every text label, image, and data point reflects the content source manifest above — no numbered generic items, no filler text, no dummy text, no empty strings.
- [ ] **Token fidelity:** colors come from the uploaded design system (primary/secondary/surface/etc.) by name; spacing comes from declared scale tokens. No invented hex codes, no invented size literals.
- [ ] **Component vocabulary:** every component in the render maps to a named design-system component (Card, FAB, BottomBar, etc.) — no invented or off-system components.
- [ ] **Archetype honored:** the layout follows the "screen" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
