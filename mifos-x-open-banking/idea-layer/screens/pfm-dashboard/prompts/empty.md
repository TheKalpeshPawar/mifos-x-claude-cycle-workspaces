---
ui_yaml_sha: 2e4309c4e8a1dd98270c9eaf453b90a7ea89bd8892ac2e21d0fdcca98cf3cd2c
design_md_hash: 2b17083785e7e532a1554540e628db54640dfab77857b6c90d802767add94ba2
app_shell_hash: d2fe35b34f2ccfe703fcea97291ff9cb0453b148553d7b69b40f4cfa59d08766
design_read_hash: 60a4c95f7619b31daccc130861a96508d0cacf2f29734f43c35036c1f0280375
content_hash: ee2d3dd5fa10b423cdcb98d3973f2107e6f5a07b90273d0c079661811d6c4649

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: pfm-dashboard
state: empty
state_visibility: empty

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# pfm-dashboard — empty state

> Auto-generated from screens/pfm-dashboard/ui.yaml @ SHA 18adbe9806a4bef1
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: dashboard

## Layout
- type: scrollable_column
- padding: default
- alignment: start

## Composition (top → bottom)
1. **text** (#pfm_title) — label: "Spending Insights", content: "Spending Insights"
2. **chip** (#pfm_scope_chip) — label: "All personal accounts · 3 accounts · GBP", content: "All personal accounts · 3 accounts · GBP"
3. **stack** (#period_selector_row) — label: "Period selector row"
4. **chip** (#period_chip_this_month) — label: "This Month", content: "This Month"
5. **chip** (#period_chip_last_month) — label: "Last Month", content: "Last Month"
6. **chip** (#period_chip_last_3_months) — label: "Last 3 Months", content: "Last 3 Months"
7. **chip** (#period_chip_custom) — label: "Custom", content: "Custom"
8. **text** (#pfm_period_label) — label: "May 2026", content: "May 2026"
9. **box** (#pfm_summary_card) — label: "Summary card", content: "Summary"
10. **text** (#summary_section_label) — label: "Summary", content: "Summary"
11. **stack** (#summary_metrics_row) — label: "Summary metrics row"
12. **text** (#spent_label) — label: "Total Spent", content: "Total Spent"
13. **text** (#spent_amount) — label: "Total spent amount (dynamic)", content: "-£820.40"
14. **text** (#received_label) — label: "Received", content: "Received"
15. **text** (#received_amount) — label: "Received amount (dynamic)", content: "£3,200.00"
16. **text** (#net_label) — label: "Net", content: "Net"
17. **text** (#net_amount) — label: "Net amount (dynamic)", content: "+£2,379.60"
18. **box** (#overall_budget_card) — label: "Monthly budget card", content: "Monthly Budget"
19. **stack** (#overall_budget_header_row) — label: "Overall budget header row"
20. **text** (#overall_budget_title) — label: "Monthly Budget", content: "Monthly Budget"
21. **text** (#overall_budget_percent) — label: "Percent used (dynamic)", content: "55% used"
22. **stack** (#overall_budget_amounts_row) — label: "Overall budget amounts row"
23. **text** (#overall_budget_spent) — label: "Spent amount (dynamic)", content: "£820.40 spent"
24. **text** (#overall_budget_remaining) — label: "Remaining amount (dynamic)", content: "£679.60 left"
25. **progress_bar** (#overall_budget_progress) — label: "Overall budget progress (dynamic)"
26. **text** (#overall_budget_of_total) — label: "Of total budget (dynamic)", content: "of £1,500.00 monthly budget — tap to change"
27. **box** (#no_budget_set_banner) — label: "No budget set banner", content: "No budget set"
28. **text** (#no_budget_banner_title) — label: "No budget set", content: "No budget set"
29. **text** (#no_budget_banner_body) — label: "Set a monthly budget to track how much you spend against your target. Tap to set", content: "Set a monthly budget to track how much you spend against your target. Tap to set"
30. **text** (#category_section_label) — label: "Spending by Category", content: "Spending by Category"
31. **box** (#category_card) — label: "Category breakdown card", content: "Category breakdown"
32. **chart** (#category_donut_chart) — label: "Spending donut chart (dynamic)", content: "Spending by category donut"
33. **list** (#category_legend_list) — label: "Category legend (dynamic, one row per category)", content: "Category legend"
34. **list_item** (#category_legend_row) — label: "Category legend row (template, dynamic)", content: "{category.label} {category.amount}"
35. **text** (#budgets_section_label) — label: "Budget Progress", content: "Budget Progress"
36. **box** (#budget_rows_card) — label: "Budget progress card", content: "Budget progress"
37. **list** (#budget_rows_list) — label: "Budget rows (dynamic, one row per category)", content: "Budget rows"
38. **list_item** (#budget_progress_row) — label: "Budget progress row (template, dynamic)", content: "{row.label} {row.spent} / {row.limit}"
39. **text** (#merchants_section_label) — label: "Top Merchants", content: "Top Merchants"
40. **box** (#merchants_card) — label: "Top merchants card", content: "Top merchants"
41. **list** (#merchants_list) — label: "Merchant rows (dynamic, top 5)", content: "Merchant rows"
42. **list_item** (#merchant_row) — label: "Merchant row (template, dynamic)", content: "{merchant.name} {merchant.amount}"
43. **button** (#view_all_transactions_button) — label: "View All Transactions", content: "View All Transactions"
44. **box** (#no_activity_state) — label: "No activity placeholder", content: "No transaction history yet"
45. **icon** (#no_activity_icon) — label: "Receipt icon", content: "receipt_long"
46. **text** (#no_activity_title) — label: "No transaction history yet", content: "No transaction history yet"
47. **text** (#no_activity_body) — label: "Your spending insights will appear once you have transactions in the selected pe", content: "Your spending insights will appear once you have transactions in the selected pe"

## State-specific behavior
- Show an empty-state illustration, a friendly message, and one primary call-to-action button.

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

- [ ] **Per-state shape:** the render shows ONLY this state ("empty"). Do not blend multiple states into one mockup.
- [ ] **Real content:** every text label, image, and data point reflects the content source manifest above — no numbered generic items, no filler text, no dummy text, no empty strings.
- [ ] **Token fidelity:** colors come from the uploaded design system (primary/secondary/surface/etc.) by name; spacing comes from declared scale tokens. No invented hex codes, no invented size literals.
- [ ] **Component vocabulary:** every component in the render maps to a named design-system component (Card, FAB, BottomBar, etc.) — no invented or off-system components.
- [ ] **Archetype honored:** the layout follows the "dashboard" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
