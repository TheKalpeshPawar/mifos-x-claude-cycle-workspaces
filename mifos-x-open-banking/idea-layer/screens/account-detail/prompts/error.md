---
ui_yaml_sha: 15c9f68a64c1f15bc328ea0656e9d6d61615f7587eddba11fb1d327e95609d5b
design_md_hash: 2b17083785e7e532a1554540e628db54640dfab77857b6c90d802767add94ba2
app_shell_hash: d2fe35b34f2ccfe703fcea97291ff9cb0453b148553d7b69b40f4cfa59d08766
design_read_hash: 60a4c95f7619b31daccc130861a96508d0cacf2f29734f43c35036c1f0280375
content_hash: 8fe3a7e3174d5ae00a30bcfb4a8c84750dd3587c17eeebc9b143d2e260950ff0

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: account-detail
state: error
state_visibility: error

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# account-detail — error state

> Auto-generated from screens/account-detail/ui.yaml @ SHA 2d9ede295e7cfa55
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: detail_screen

## Layout
- type: scrollable_column
- padding: default
- alignment: start

## Composition (top → bottom)
1. **box** (#account_header_card) — "account_header_card"
   - **text** (#account_header_label) — content: "Everyday Current"
   - **text** (#account_header_balance) — content: "£4,250.00"
   - **box** (#account_currency_badge) — "account_currency_badge"
      - **text** (#account_currency_label) — content: "GBP"
2. **text** (#activity_group_label) — content: "ACTIVITY"
3. **box** (#activity_transactions_row) — "activity_transactions_row"
   - **stack** (#activity_txn_row) — "activity_txn_row"
      - **stack** (#activity_txn_text_col) — "activity_txn_text_col"
         - **text** (#activity_txn_title) — content: "Transaction history"
         - **text** (#activity_txn_subtitle) — content: "Booked and pending payments"
      - **icon** (#activity_txn_chevron) — content: "chevron_right"
4. **box** (#activity_direct_debits_row) — "activity_direct_debits_row"
   - **stack** (#activity_dd_row) — "activity_dd_row"
      - **stack** (#activity_dd_text_col) — "activity_dd_text_col"
         - **text** (#activity_dd_title) — content: "Direct debits"
         - **text** (#activity_dd_subtitle) — content: "Mandates collecting from this account"
      - **icon** (#activity_dd_chevron) — content: "chevron_right"
5. **text** (#routing_group_label) — content: "ACCOUNT & ROUTING"
6. **box** (#account_info_card) — "account_info_card"
   - **stack** (#holder_row) — "holder_row"
      - **text** (#holder_label) — content: "Account Holder"
      - **text** (#holder_value) — content: "Eve Adamson"
   - **divider** (#info_divider_1)
   - **stack** (#number_row) — "number_row"
      - **stack** (#number_label_col) — "number_label_col"
         - **text** (#number_label) — content: "Account Number"
         - **text** (#number_value) — content: "20294393"
      - **icon** (#copy_number_button) — content: "content_copy"
   - **divider** (#info_divider_2)
   - **stack** (#iban_row) — "iban_row"
      - **stack** (#iban_label_col) — "iban_label_col"
         - **text** (#iban_label) — content: "IBAN"
         - **text** (#iban_value) — content: "GB29 MFOS 2029 4393 0000 00"
      - **icon** (#copy_iban_button) — content: "content_copy"
   - **divider** (#info_divider_3)
   - **stack** (#bank_row) — "bank_row"
      - **text** (#bank_label) — content: "Bank"
      - **text** (#bank_value) — content: "Mifos Bank UK"
7. **text** (#plan_group_label) — content: "PLAN & FEES"
8. **box** (#account_plan_card) — "account_plan_card"
   - **stack** (#product_row) — "product_row"
      - **text** (#product_label) — content: "Product"
      - **text** (#product_value) — content: "Business Current GBP"
   - **divider** (#plan_divider_1)
   - **stack** (#attribute_row_1) — "attribute_row_1"
      - **text** (#attribute_1_label) — content: "Monthly Fee"
      - **text** (#attribute_1_value) — content: "£25.00"
9. **spacer** (#bottom_spacer)

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
- [ ] **Archetype honored:** the layout follows the "detail_screen" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
