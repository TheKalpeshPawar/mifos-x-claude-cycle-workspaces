---
ui_yaml_sha: 3747e8c19a3ae10585439a8bc5107c3be3bd474302e2738ad1672d41544a35e8
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 522836fb57eca2f8d9be37870af6d3693a92ec2c9f7b643c51c07ff5f51311fa

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: statements
state: error
state_visibility: error

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# statements — error state

> Auto-generated from screens/statements/ui.yaml @ SHA 9a6fc50574e98dbf
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the error state of the statements screen for **HSBC Open Banking**, a UK AISP reference app that failed to load OBReadStatement2 data from HSBC, within the Trust Blue minimalist Material 3 dark system on a 393x852dp Pixel 5.

Palette: primary #95CDF7, onPrimary #00344E, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, error #FFB4AB, onSurfaceVariant #C1C7CE, errorContainer #93000A, onErrorContainer #FFDAD6, outline #8B9198

**Component 1 - Top App Bar** (full width, 64dp, bg #101417): back-arrow icon 24dp #95CDF7 left; title Outfit medium 22sp "Statements" #E0E3E8.

**Component 2 - Error State** (361dp wide, vertically centered in remaining height, centered, generous vertical breathing room): error-outline icon 64dp #FFB4AB centered; Outfit medium 20sp "Could not load statements" #E0E3E8 below icon, 16dp gap; Outfit regular 14sp "HSBC returned an error when fetching your statements. Check your connection and try again." #C1C7CE centered, max 2 lines; 24dp gap below body. This is the error_state archetype.

**Component 3 - Button** (200dp wide, 48dp height, r=full, bg #95CDF7, label Outfit medium 16sp "Try again" #00344E): centered horizontally below the error message.

**Component 4 - Bottom Navigation Bar** (full width, 80dp, bg #1C2024): items "Home", "Accounts", "Statements", "More"; "Statements" filled icon #95CDF7; inactive #C1C7CE.

Do not show a list skeleton or any statement period rows behind the error component; only the error icon, message, and Retry button are visible. Do not use #FFB4AB as the Retry button container; the button is filled primary #95CDF7 with #00344E label only. Do not include an HTTP status code or API diagnostic string in the user-facing message; plain English recovery copy only. Do not add a secondary action or "contact support" link; one Retry button only.

Composed failure. Single recovery action. Regulated fintech dignity. Tone: calm, #95CDF7 minimal.

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

- [ ] **Per-state shape:** the render shows ONLY this state ("error"). Do not blend multiple states into one mockup.
- [ ] **Real content:** every text label, image, and data point reflects the content source manifest above — no numbered generic items, no filler text, no dummy text, no empty strings.
- [ ] **Token fidelity:** colors come from the uploaded design system (primary/secondary/surface/etc.) by name; spacing comes from declared scale tokens. No invented hex codes, no invented size literals.
- [ ] **Component vocabulary:** every component in the render maps to a named design-system component (Card, FAB, BottomBar, etc.) — no invented or off-system components.
- [ ] **Archetype honored:** the layout follows the "screen" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
