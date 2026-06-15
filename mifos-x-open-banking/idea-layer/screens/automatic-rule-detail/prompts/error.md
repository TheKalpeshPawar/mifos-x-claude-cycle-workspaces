---
ui_yaml_sha: 9fb58509d5b0516fef0ddacc3f2bb6d4c3e1748a2018c3270bcc6cd1b595e71d
design_md_hash: 2b17083785e7e532a1554540e628db54640dfab77857b6c90d802767add94ba2
app_shell_hash: 33fdcb113930d6c243094587e9fb8386d41a289204b1484e98129c79f97bea84
design_read_hash: 60a4c95f7619b31daccc130861a96508d0cacf2f29734f43c35036c1f0280375
content_hash: 72b6b593f6cdcab15d3c0188780309d7074e289300c42369e79c6099e1c27d8f

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: automatic-rule-detail
state: error
state_visibility: error

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# automatic-rule-detail — error state

> Auto-generated from screens/automatic-rule-detail/ui.yaml @ SHA 8fc32a116a29df9e
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: detail

## Layout
- type: scrollable_column
- padding: default
- alignment: start

## Composition (top → bottom)
1. **text** (#rule_name) — label: "Rule name", content: "Round-up to Rainy Day Saver"
2. **badge** (#status_pill) — label: "Status", content: "● ACTIVE"
3. **box** (#limits_card) — label: "Limits", content: "Max £50 per payment · £200 per month · Valid until 20 May 2027"
4. **text** (#activity_header) — label: "Recent payments", content: "RECENT PAYMENTS"
5. **list_item** (#activity_row) — label: "Automatic payment", content: "£12.40 to Rainy Day Saver"
6. **text** (#activity_subtitle) — label: "Date", content: "12 June · Round-up"
7. **button** (#revoke_button) — label: "Revoke rule"
8. **text** (#revoke_note) — label: "Revoke note", content: "Revoking stops all future automatic payments immediately. Money already moved st"

## State-specific behavior
- Show an error illustration, a short message, and a single Retry action. No content rails visible.

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
- [ ] **Archetype honored:** the layout follows the "detail" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
