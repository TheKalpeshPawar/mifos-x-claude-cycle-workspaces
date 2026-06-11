---
ui_yaml_sha: 38a15c4cf7bc2c6f619ed8622965a7de0f0a6430f5f64b69de9858bc7369dd62
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 2e989112615799cc5236d9be9e02307bcb4fa0d21ded257211de4e55f5a17f35

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: dashboard

feature: business-insights
state: populated
state_visibility: populated

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# business-insights — populated state

> Auto-generated from screens/business-insights/ui.yaml @ SHA ac881533c2aa31cb
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: dashboard

## Layout
- type: scrollable_column
- padding: default
- alignment: start

## Composition (top → bottom)
1. **chip** (#biz_account_selector) — label: "Business account selector", content: "TechStart — Business Current GBP"
2. **stack** (#biz_period_selector_row) — label: "Period selector row"
3. **text** (#biz_period_label) — label: "Period label", content: "June 2026"
4. **card** (#biz_cash_flow_card) — "biz_cash_flow_card"
   - **stack** (#biz_cash_flow_row) — "biz_cash_flow_row"
      - **text** (#biz_money_in) — label: "Money In", content: "£75000.00"
      - **text** (#biz_money_out) — label: "Money Out", content: "-£26300.00"
      - **text** (#biz_net) — label: "Net", content: "£48700.00"
5. **text** (#biz_expenses_title) — label: "Expenses section title", content: "Expenses by Category"
6. **card** (#biz_expense_donut_card) — "biz_expense_donut_card"
   - **list_item** (#biz_category_payroll) — label: "Payroll & Contractors", content: "Payroll & Contractors — -£15516.01"
   - **list_item** (#biz_category_tax) — label: "Tax", content: "Tax — -£8000.00"
   - **list_item** (#biz_category_rent) — label: "Rent & Facilities", content: "Rent & Facilities — -£2500.00"
   - **list_item** (#biz_category_software) — label: "Software & Subscriptions", content: "Software & Subscriptions — -£450.00"
   - **list_item** (#biz_category_insurance) — label: "Insurance", content: "Insurance — -£350.00"
7. **text** (#biz_merchants_title) — label: "Top counterparties title", content: "Top Counterparties"
8. **card** (#biz_merchants_card) — "biz_merchants_card"
   - **list_item** (#biz_merchant_payroll) — label: "Mifos-X-Open-Bank payroll", content: "Mifos-X-Open-Bank — 1 payment — -£15000.00"

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

- [ ] **Per-state shape:** the render shows ONLY this state ("populated"). Do not blend multiple states into one mockup.
- [ ] **Real content:** every text label, image, and data point reflects the content source manifest above — no numbered generic items, no filler text, no dummy text, no empty strings.
- [ ] **Token fidelity:** colors come from the uploaded design system (primary/secondary/surface/etc.) by name; spacing comes from declared scale tokens. No invented hex codes, no invented size literals.
- [ ] **Component vocabulary:** every component in the render maps to a named design-system component (Card, FAB, BottomBar, etc.) — no invented or off-system components.
- [ ] **Archetype honored:** the layout follows the "dashboard" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
