---
ui_yaml_sha: 684768322b49a1aba4627c9ccf014470377e0bfce875ce8dfcaf08bcccf91bb5
design_md_hash: 2b17083785e7e532a1554540e628db54640dfab77857b6c90d802767add94ba2
app_shell_hash: d2fe35b34f2ccfe703fcea97291ff9cb0453b148553d7b69b40f4cfa59d08766
design_read_hash: 60a4c95f7619b31daccc130861a96508d0cacf2f29734f43c35036c1f0280375
content_hash: 1f18308f75c69d1ddeab87f20a5b647bd10a993e4714e32d38d7b2c1b7bcc97a

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: form

feature: standing-order-edit
state: content
state_visibility: content

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# standing-order-edit — content state

> Auto-generated from screens/standing-order-edit/ui.yaml @ SHA f4bd68a33178c4fc
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: form

## Layout
- type: column
- padding: spacing.md
- alignment: start

## Composition (top → bottom)
1. **stack** (#soe_root)
2. **card** (#soe_beneficiary_card)
3. **text** (#soe_beneficiary_header) — content: "Paying To"
4. **stack** (#soe_beneficiary_row)
5. **icon** (#soe_beneficiary_icon) — content: "account_balance"
6. **stack** (#soe_beneficiary_info)
7. **text** (#soe_beneficiary_name) — content: "Landlord Holdings Ltd"
8. **text** (#soe_beneficiary_iban) — content: "GB29 NWBK 6016 1331 9268 19 · NatWest Bank"
9. **input** (#soe_amount_input) — label: "Amount", content: "1200.00"
10. **input** (#soe_currency_selector) — label: "Currency", content: "GBP — British Pound"
11. **input** (#soe_frequency_selector) — label: "Frequency", content: "Monthly"
12. **input** (#soe_start_date_input) — label: "Start Date", content: "1 Jan 2026"
13. **input** (#soe_end_date_input) — label: "End Date (optional)", content: "Ongoing — no end date"
14. **banner** (#soe_error_banner) — content: "Couldn't save your changes. Check the amount and try again."
15. **button** (#soe_save_button) — label: "Save Changes"
16. **button** (#soe_cancel_button) — label: "Cancel"
17. **spacer** (#soe_bottom_spacer)
18. **loading_indicator** (#soe_saving_indicator)

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
- [ ] **Archetype honored:** the layout follows the "form" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
