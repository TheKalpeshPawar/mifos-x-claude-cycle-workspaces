---
ui_yaml_sha: 60ea889089402b77212862950b00bc23d2df6eab0bb5a73dcc30299e66174c79
design_md_hash: 2b17083785e7e532a1554540e628db54640dfab77857b6c90d802767add94ba2
app_shell_hash: d2fe35b34f2ccfe703fcea97291ff9cb0453b148553d7b69b40f4cfa59d08766
design_read_hash: 60a4c95f7619b31daccc130861a96508d0cacf2f29734f43c35036c1f0280375
content_hash: ea3cb2f274d1353ff09eb7ed3dfa8b393224f1a4c48adba84d741ef8dc76aabe

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: index_list

feature: pay
state: content
state_visibility: content

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# pay — content state

> Auto-generated from screens/pay/ui.yaml @ SHA 4cbd503cd2c7e428
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: index_list

## Layout
- type: scrollable_column
- padding: default
- alignment: start

## Composition (top → bottom)
1. **text** (#kind_chooser_header) — label: "How would you like to pay?", content: "HOW WOULD YOU LIKE TO PAY?"
2. **list_item** (#kind_now) — label: "Pay now", content: "Pay now"
3. **list_item** (#kind_scheduled) — label: "Scheduled payment", content: "Scheduled payment"
4. **list_item** (#kind_recurring) — label: "Recurring payment", content: "Recurring payment"
5. **text** (#from_account_header) — label: "From account", content: "FROM ACCOUNT"
6. **list_item** (#account_selector) — label: "From account", content: "Primary Checking — €4,820.00"
7. **text** (#recent_recipients_header) — label: "Recent Recipients", content: "RECENT RECIPIENTS"
8. **box** (#recipient_new) — label: "New", content: "New"
9. **box** (#recent_recipient_item) — label: "Recent recipient", content: "LW"
10. **text** (#all_beneficiaries_header) — label: "All Beneficiaries", content: "ALL BENEFICIARIES"
11. **list_item** (#beneficiary_item) — label: "Beneficiary", content: "Liam Walker"
12. **text** (#beneficiary_subtitle) — label: "SEPA · Afternoon Coffee Bank ·· 8842", content: "SEPA · Afternoon Coffee Bank ·· 8842"
13. **text** (#no_beneficiaries_note) — label: "No payees on this account yet", content: "No payees on this account yet. Switch accounts above."

## State-specific behavior
- Fully populated with the real demo content listed below.

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
- [ ] **Archetype honored:** the layout follows the "index_list" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
