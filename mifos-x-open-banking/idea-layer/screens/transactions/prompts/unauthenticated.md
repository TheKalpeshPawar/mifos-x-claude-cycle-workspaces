---
ui_yaml_sha: 0da41b7a35a4d1f08fa17c6881bb83b8b5305cc638d12fcd18a48fea300331b5
design_md_hash: 2b17083785e7e532a1554540e628db54640dfab77857b6c90d802767add94ba2
app_shell_hash: d2fe35b34f2ccfe703fcea97291ff9cb0453b148553d7b69b40f4cfa59d08766
design_read_hash: 60a4c95f7619b31daccc130861a96508d0cacf2f29734f43c35036c1f0280375
content_hash: 3d5995ca094f7cdca87fda1b48b15777ea5f24237ceb6a5f523d16a9de8eca85

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: index_list

feature: transactions
state: unauthenticated
state_visibility: unauthenticated

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# transactions — unauthenticated state

> Auto-generated from screens/transactions/ui.yaml @ SHA 84d868506b291dcd
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: index_list

## Layout
- type: scrollable_column
- padding: default
- alignment: start

## Composition (top → bottom)
1. **input** (#search_bar)
2. **stack** (#date_chips_row) — "date_chips_row"
   - **chip** (#range_chip_last_7_days) — label: "7 days"
   - **chip** (#range_chip_last_30_days) — label: "30 days"
   - **chip** (#range_chip_last_60_days) — label: "60 days"
   - **chip** (#range_chip_last_90_days) — label: "90 days"
   - **chip** (#range_chip_custom) — label: "Custom"
3. **dialog** (#date_range_picker_dialog) — label: "Custom date range picker"
4. **stack** (#filter_chips_row) — "filter_chips_row"
   - **button** (#filter_all) — label: "All"
   - **button** (#filter_debit) — label: "Debit"
   - **button** (#filter_credit) — label: "Credit"
   - **button** (#filter_pending) — label: "Pending"
5. **box** (#monthly_summary_card) — "monthly_summary_card"
   - **stack** (#monthly_summary_row) — "monthly_summary_row"
      - **stack** (#spent_col) — "spent_col"
         - **text** (#spent_label) — content: "Spent this month"
         - **text** (#spent_amount) — content: "£1,240.30"
      - **box** (#summary_divider_v)
      - **stack** (#received_col) — "received_col"
         - **text** (#received_label) — content: "Received"
         - **text** (#received_amount) — content: "£3,200.00"
6. **text** (#pending_section_header) — content: "PENDING"
7. **box** (#pending_row_1) — "pending_row_1"
   - **stack** (#pending1_main_row) — "pending1_main_row"
      - **icon** (#pending1_icon) — content: "schedule"
      - **stack** (#pending1_info) — "pending1_info"
         - **text** (#pending1_name) — content: "Octopus Energy"
         - **text** (#pending1_status) — content: "Awaiting confirmation"
      - **text** (#pending1_amount) — content: "£64.12"
8. **text** (#transactions_date_group_header) — content: "25 May 2026"
9. **box** (#txn_list_row_1) — "txn_list_row_1"
   - **stack** (#txn1_main_row) — "txn1_main_row"
      - **image** (#txn1_merchant_logo) — content: "merchant_tesco"
      - **stack** (#txn1_info) — "txn1_info"
         - **text** (#txn1_name) — content: "Tesco Supermarket"
         - **stack** (#txn1_meta_row) — "txn1_meta_row"
            - **text** (#txn1_date_meta) — content: "25 May 2026"
            - **text** (#txn1_dot) — content: "·"
            - **box** (#txn1_category_badge) — "txn1_category_badge"
               - **text** (#txn1_category) — content: "Groceries"
      - **text** (#txn1_amount_col) — content: "-£42.50"
10. **box** (#txn_list_row_2) — "txn_list_row_2"
   - **stack** (#txn2_main_row) — "txn2_main_row"
      - **image** (#txn2_merchant_logo) — content: "merchant_bank_transfer"
      - **stack** (#txn2_info) — "txn2_info"
         - **text** (#txn2_name) — content: "Salary Payment"
         - **stack** (#txn2_meta_row) — "txn2_meta_row"
            - **text** (#txn2_date_meta) — content: "24 May 2026"
            - **text** (#txn2_dot) — content: "·"
            - **box** (#txn2_category_badge) — "txn2_category_badge"
               - **text** (#txn2_category) — content: "Income"
      - **text** (#txn2_amount_col) — content: "+£3,200.00"
11. **box** (#txn_list_row_3) — "txn_list_row_3"
   - **stack** (#txn3_main_row) — "txn3_main_row"
      - **image** (#txn3_merchant_logo) — content: "merchant_edf"
      - **stack** (#txn3_info) — "txn3_info"
         - **text** (#txn3_name) — content: "EDF Energy"
         - **stack** (#txn3_meta_row) — "txn3_meta_row"
            - **text** (#txn3_date_meta) — content: "23 May 2026"
            - **text** (#txn3_dot) — content: "·"
            - **box** (#txn3_category_badge) — "txn3_category_badge"
               - **text** (#txn3_category) — content: "Utilities"
      - **text** (#txn3_amount_col) — content: "-£94.20"
12. **button** (#load_more_button) — label: "Load More Transactions"
13. **spacer** (#bottom_spacer)

## State-specific behavior
- Custom state "Unauthenticated" — render per the composition below.

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

- [ ] **Per-state shape:** the render shows ONLY this state ("unauthenticated"). Do not blend multiple states into one mockup.
- [ ] **Real content:** every text label, image, and data point reflects the content source manifest above — no numbered generic items, no filler text, no dummy text, no empty strings.
- [ ] **Token fidelity:** colors come from the uploaded design system (primary/secondary/surface/etc.) by name; spacing comes from declared scale tokens. No invented hex codes, no invented size literals.
- [ ] **Component vocabulary:** every component in the render maps to a named design-system component (Card, FAB, BottomBar, etc.) — no invented or off-system components.
- [ ] **Archetype honored:** the layout follows the "index_list" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
