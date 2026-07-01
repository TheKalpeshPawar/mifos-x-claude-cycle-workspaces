---
ui_yaml_sha: 3747e8c19a3ae10585439a8bc5107c3be3bd474302e2738ad1672d41544a35e8
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: ca1ce4551ae8654d4382214554659d093b9b058b0a041afa2401da701ad5f792

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: statements
state: empty
state_visibility: empty

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# statements — empty state

> Auto-generated from screens/statements/ui.yaml @ SHA 1e57c7bdbf571f3e
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the empty state of the statements screen for **HSBC Open Banking**, a UK AISP reference app confirming no OBReadStatement2 records are available for this HSBC account, within the Trust Blue minimalist Material 3 dark system on a 393x852dp Pixel 5.

Palette: primary #95CDF7, onPrimary #00344E, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, error #FFB4AB, onSurfaceVariant #C1C7CE, outline #8B9198, primaryContainer #004B6F, secondary #B7C9D9

**Component 1 - Top App Bar** (full width, 64dp, bg #101417): back-arrow icon 24dp #95CDF7 left; title Outfit medium 22sp "Statements" #E0E3E8.

**Component 2 - Empty State** (361dp wide, vertically centered in remaining height, centered, generous vertical breathing room): description-outline icon 64dp #95CDF7 centered; Outfit medium 20sp "No statements available" #E0E3E8 below icon, 16dp gap; Outfit regular 14sp "No statements have been generated for this HSBC account. Statements typically appear after your first full billing period." #C1C7CE centered, 2-line max; no CTA button. This is the empty_state archetype.

**Component 3 - Bottom Navigation Bar** (full width, 80dp, bg #1C2024): items "Home", "Accounts", "Statements", "More"; "Statements" filled icon #95CDF7; inactive #C1C7CE.

Do not add a CTA to request or generate a statement; AISP has read-only access and no power to create statements. Do not use a decorative scene illustration or graphic beyond the single description icon; low-variance minimalist-ui. Do not apply warm tones, amber, or green to the empty state; cool trust-blue palette only. Do not frame the absence of statements as a failure; the copy explains the standard billing cycle without alarm.

Honest confirmation. No statements generated yet. Read-only AISP clarity. Tone: restrained, #95CDF7 minimal.

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
