---
ui_yaml_sha: d43f94dd47be443c1f05709d9c7d049415d8f1145c0f08cf6f9140173c24dc9c
design_md_hash: 2b17083785e7e532a1554540e628db54640dfab77857b6c90d802767add94ba2
app_shell_hash: d2fe35b34f2ccfe703fcea97291ff9cb0453b148553d7b69b40f4cfa59d08766
design_read_hash: 60a4c95f7619b31daccc130861a96508d0cacf2f29734f43c35036c1f0280375
content_hash: 79b170a6cf514ab56936bcbe1f3fd068e0024f1129da6efe8500aaf25e6409ae

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: form

feature: send-money-amount
state: content
state_visibility: content

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# send-money-amount — content state

> Auto-generated from screens/send-money-amount/ui.yaml @ SHA 561d05aad7176970
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: form

## Layout
- type: scrollable_column
- padding: default
- alignment: start

## Composition (top → bottom)
1. **list_item** (#from_account_selector) — label: "From Account", content: "Primary Checking — €4,820.00"
2. **input** (#amount_input) — label: "Amount"
3. **text** (#to_label) — label: "To", content: "To"
4. **input** (#beneficiary_search) — label: "Search beneficiary"
5. **list_item** (#beneficiary_row) — label: "Beneficiary", content: "Liam Walker"
6. **input** (#reference_input) — label: "Reference"
7. **text** (#payment_type_label) — label: "Payment Type", content: "Payment Type"
8. **chip_group** (#payment_type_chips) — label: "Payment rail", content: "SEPA · Domestic · International"
9. **text** (#rail_ineligible_reason) — label: "Rail unavailable reason", content: "International unavailable — no BIC on file for this beneficiary"
10. **box** (#fee_banner) — label: "Estimated fee", content: "Estimated fee: Free (SEPA)"
11. **text** (#internal_transfer_note) — label: "Internal bank transfer note", content: "Internal bank transfer — sent instantly within the bank."
12. **text** (#sandbox_block_reason) — label: "Sandbox block reason", content: "On the sandbox, amounts this large can only be sent to accounts within the bank."
13. **button** (#continue_button) — label: "Continue"

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
- [ ] **Archetype honored:** the layout follows the "form" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
