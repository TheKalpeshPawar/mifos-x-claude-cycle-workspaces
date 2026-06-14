---
ui_yaml_sha: 619527dcd0093145ca15e7e9b0b8cf1cc5e10850a4f4720c216cd9268d263ffc
design_md_hash: 2b17083785e7e532a1554540e628db54640dfab77857b6c90d802767add94ba2
app_shell_hash: d2fe35b34f2ccfe703fcea97291ff9cb0453b148553d7b69b40f4cfa59d08766
design_read_hash: 60a4c95f7619b31daccc130861a96508d0cacf2f29734f43c35036c1f0280375
content_hash: 3ae66372e6715db0a84babf9a29cedd8db3039c8f440d10152a4b1b4b0e5d8c2

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: confirmation

feature: payment-result
state: content
state_visibility: content

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# payment-result — content state

> Auto-generated from screens/payment-result/ui.yaml @ SHA 7a31d0ee5084cafa
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: confirmation

## Layout
- type: scrollable_column
- padding: default
- alignment: start

## Composition (top → bottom)
1. **card** (#hero_card) — label: "Payment success hero", content: "Payment sent"
2. **icon** (#success_check) — label: "Success check", content: "check"
3. **text** (#result_title) — label: "Payment sent", content: "Payment sent"
4. **text** (#result_summary) — label: "Amount to beneficiary", content: "€250.00 to Liam Walker"
5. **badge** (#status_pill) — label: "Status pill", content: "● COMPLETED"
6. **card** (#details_card) — label: "Transaction details"
7. **stack** (#transaction_id_row) — label: "Transaction ID row", content: "Transaction ID  99888bf1-69aa…"
8. **divider** (#details_divider)
9. **stack** (#from_row) — label: "From row", content: "From  Primary Checking"
10. **stack** (#charge_row) — label: "Charge row", content: "Charge  €0.00"
11. **stack** (#posted_row) — label: "Posted row", content: "Posted  Just now"
12. **button** (#view_transaction_button) — label: "View transaction"
13. **button** (#done_button) — label: "Done"

## State-specific behavior
- Fully populated with the real demo content listed below. This is the screen's initial state.

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
- [ ] **Archetype honored:** the layout follows the "confirmation" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
