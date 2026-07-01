---
ui_yaml_sha: 3747e8c19a3ae10585439a8bc5107c3be3bd474302e2738ad1672d41544a35e8
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 352e4c2fe66705f0fdd1dffa0ee7b304e7c76a0a46963d12dee109c2d12c61ea

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: statements
state: content
state_visibility: content

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# statements — content state

> Auto-generated from screens/statements/ui.yaml @ SHA 70b1535ef722b74f
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the statements screen for **HSBC Open Banking**, a UK AISP reference app listing OBReadStatement2 statement periods for an HSBC current account, within the Trust Blue minimalist Material 3 dark system on a 393x852dp Pixel 5.

Palette: primary #95CDF7, onPrimary #00344E, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, error #FFB4AB, onSurfaceVariant #C1C7CE, outline #8B9198, outlineVariant #41474D, secondary #B7C9D9

**Component 1 - Top App Bar** (full width, 64dp, bg #101417): back-arrow icon 24dp #95CDF7 left, 48dp touch target; title Outfit medium 22sp "Statements" #E0E3E8; no elevation.

**Component 2 - Chip Row** (full width, 40dp, bg #101417, below top bar, 16dp left padding): single "Regular" chip Outfit 12sp #B7C9D9, bg #384956, r=full; indicates OBReadStatement2 StatementType.

**Component 3 - List** (full width minus 32dp insets, scrollable, bg #101417): 6 rows each 72dp tall, 1dp #41474D dividers between rows; archetype detail_screen. Row 1: Outfit medium 16sp "June 2026" #E0E3E8 left, Outfit regular 14sp "01 Jun 2026 - 30 Jun 2026" #C1C7CE below, chevron-right 20dp #8B9198 right. Row 2: "May 2026", "01 May 2026 - 31 May 2026". Row 3: "April 2026", "01 Apr 2026 - 30 Apr 2026". Row 4: "March 2026", "01 Mar 2026 - 31 Mar 2026". Row 5: "February 2026", "01 Feb 2026 - 28 Feb 2026". Row 6: "January 2026", "01 Jan 2026 - 31 Jan 2026". Each row tappable to statement-detail.

**Component 4 - Bottom Navigation Bar** (full width, 80dp, bg #1C2024): items "Home", "Accounts", "Statements", "More"; "Statements" filled icon and label #95CDF7; inactive #C1C7CE.

Do not display financial balances, totals, or any monetary amounts at list-row level; period rows show date range and type only. Do not add a download button at the list level; PDF download action belongs on the statement-detail screen only. Do not render elevated Cards for rows; flat list rows on #101417 with 1dp #41474D dividers, no card shadow. Do not show the StatementId reference code in any row; human-readable month label and date range only.

Legible archive. Six HSBC statement periods at a glance. Regulated, unhurried browsing. Tone: restrained, #95CDF7 minimal.

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

- [ ] **Per-state shape:** the render shows ONLY this state ("content"). Do not blend multiple states into one mockup.
- [ ] **Real content:** every text label, image, and data point reflects the content source manifest above — no numbered generic items, no filler text, no dummy text, no empty strings.
- [ ] **Token fidelity:** colors come from the uploaded design system (primary/secondary/surface/etc.) by name; spacing comes from declared scale tokens. No invented hex codes, no invented size literals.
- [ ] **Component vocabulary:** every component in the render maps to a named design-system component (Card, FAB, BottomBar, etc.) — no invented or off-system components.
- [ ] **Archetype honored:** the layout follows the "screen" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
