---
ui_yaml_sha: 55b996d4d35ede9a8c53106b423e52ea4fffe3554f9cc759abe914acab9272f1
design_md_hash: 2b17083785e7e532a1554540e628db54640dfab77857b6c90d802767add94ba2
app_shell_hash: d2fe35b34f2ccfe703fcea97291ff9cb0453b148553d7b69b40f4cfa59d08766
design_read_hash: 60a4c95f7619b31daccc130861a96508d0cacf2f29734f43c35036c1f0280375
content_hash: 2601dbb827bc1426c20e623db29d539c177df4849b7bf73791c2df69f440fcbe

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: standing-order-create
state: loading
state_visibility: loading

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# standing-order-create — loading state

> Auto-generated from screens/standing-order-create/ui.yaml @ SHA 57e0abac383f2d9f
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: form_screen

## Layout
- type: column
- padding: spacing.xl
- alignment: center

## Composition (top → bottom)
1. **stack** (#soc_root)
2. **input** (#soc_source_account_field) — label: "From account"
3. **bottom_sheet** (#soc_account_picker_sheet) — label: "Choose account"
4. **input** (#soc_payee_field) — label: "Pay to"
5. **menu** (#soc_payee_menu) — label: "Payee list"
6. **text** (#soc_no_payees_hint) — label: "No payees hint", content: "Add a beneficiary first — standing orders pay an existing payee."
7. **text_field** (#soc_amount_field) — label: "Amount"
8. **text** (#soc_frequency_label) — label: "Repeats", content: "Repeats"
9. **chip_group** (#soc_frequency_chips) — label: "Frequency chips"
10. **input** (#soc_start_date_field) — label: "First payment date"
11. **date_picker** (#soc_start_date_picker) — label: "Pick first payment date"
12. **text** (#soc_recurrence_hint) — label: "Recurrence hint", content: "Repeats every Monday"
13. **input** (#soc_end_date_field) — label: "End date (optional)"
14. **date_picker** (#soc_end_date_picker) — label: "Pick end date"
15. **text** (#soc_error_text) — label: "Validation / submit error", content: "Start date must be after today"
16. **button** (#soc_submit_button) — label: "Create standing order", content: "Create standing order"
17. **skeleton** (#soc_loading) — label: "Loading payees"

## State-specific behavior
- Show shimmer/skeleton loaders matching the content layout block-for-block — no real text, no images. This is the screen's initial state.

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
- [ ] **Archetype honored:** the layout follows the "form_screen" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
