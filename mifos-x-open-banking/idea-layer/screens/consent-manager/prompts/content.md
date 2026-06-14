---
ui_yaml_sha: e4043bf6fd296afbfef36c3ea112ec197f8fa18c3c813cfce7f35e45182d8415
design_md_hash: 2b17083785e7e532a1554540e628db54640dfab77857b6c90d802767add94ba2
app_shell_hash: d2fe35b34f2ccfe703fcea97291ff9cb0453b148553d7b69b40f4cfa59d08766
design_read_hash: 60a4c95f7619b31daccc130861a96508d0cacf2f29734f43c35036c1f0280375
content_hash: 389206892adf254f6afc7cc9c3c588216226588a20f38e0c27eb77f0055a6aec

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: index_list

feature: consent-manager
state: content
state_visibility: content

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# consent-manager — content state

> Auto-generated from screens/consent-manager/ui.yaml @ SHA b4b008b9f000a1de
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: index_list

## Layout
- type: scrollable_column
- padding: default
- alignment: start

## Composition (top → bottom)
1. **text** (#consent_title) — label: "Connected Apps", content: "Connected Apps"
2. **text** (#consent_subtitle) — label: "Apps you've connected and the account data each can access. Revoke access at any", content: "Apps you've connected and the account data each can access. Revoke access at any"
3. **box** (#consent_moneymanager) — label: "MoneyManager Pro consent card", content: "MoneyManager Pro consent card"
4. **stack** (#moneymanager_header_row) — label: "MoneyManager Pro header row"
5. **image** (#moneymanager_logo) — label: "MoneyManager Pro logo", content: "app_logo_moneymanager"
6. **stack** (#moneymanager_info) — label: "MoneyManager Pro app info"
7. **text** (#moneymanager_name) — label: "MoneyManager Pro", content: "MoneyManager Pro"
8. **text** (#moneymanager_dates) — label: "Granted 1 Mar 2026 · Expires 1 Mar 2027", content: "Granted 1 Mar 2026 · Expires 1 Mar 2027"
9. **box** (#moneymanager_active_badge) — label: "ACTIVE", content: "ACTIVE"
10. **stack** (#moneymanager_scopes_row) — label: "MoneyManager Pro consent scopes"
11. **box** (#moneymanager_scope_read_accounts) — label: "Account Details", content: "Account Details"
12. **box** (#moneymanager_scope_view_transactions) — label: "Transactions", content: "Transactions"
13. **box** (#moneymanager_scope_check_balances) — label: "Balances", content: "Balances"
14. **button** (#moneymanager_revoke_button) — label: "Revoke Access"
15. **box** (#consent_taxhelper) — label: "TaxHelper consent card", content: "TaxHelper consent card"
16. **stack** (#taxhelper_header_row) — label: "TaxHelper header row"
17. **image** (#taxhelper_logo) — label: "TaxHelper logo", content: "app_logo_taxhelper"
18. **stack** (#taxhelper_info) — label: "TaxHelper app info"
19. **text** (#taxhelper_name) — label: "TaxHelper", content: "TaxHelper"
20. **text** (#taxhelper_dates) — label: "Granted 15 Jan 2026 · Expires 15 Jan 2027", content: "Granted 15 Jan 2026 · Expires 15 Jan 2027"
21. **box** (#taxhelper_active_badge) — label: "ACTIVE", content: "ACTIVE"
22. **stack** (#taxhelper_scopes_row) — label: "TaxHelper consent scopes"
23. **box** (#taxhelper_scope_view_transactions) — label: "Transactions", content: "Transactions"
24. **box** (#taxhelper_scope_read_accounts) — label: "Account Details", content: "Account Details"
25. **button** (#taxhelper_revoke_button) — label: "Revoke Access"
26. **box** (#consent_budgetwise) — label: "BudgetWise consent card", content: "BudgetWise consent card"
27. **stack** (#budgetwise_header_row) — label: "BudgetWise header row"
28. **image** (#budgetwise_logo) — label: "BudgetWise logo", content: "app_logo_budgetwise"
29. **stack** (#budgetwise_info) — label: "BudgetWise app info"
30. **text** (#budgetwise_name) — label: "BudgetWise", content: "BudgetWise"
31. **text** (#budgetwise_dates) — label: "Granted 10 Oct 2025 · Expired 10 Apr 2026", content: "Granted 10 Oct 2025 · Expired 10 Apr 2026"
32. **box** (#budgetwise_expired_badge) — label: "EXPIRED", content: "EXPIRED"
33. **stack** (#budgetwise_scopes_row) — label: "BudgetWise consent scopes"
34. **box** (#budgetwise_scope_check_balances) — label: "Balances", content: "Balances"
35. **button** (#budgetwise_remove_button) — label: "Remove"
36. **button** (#disconnect_all_button) — label: "Disconnect everything"
37. **box** (#revoke_confirm_dialog) — label: "Revoke access confirmation dialog", content: "Revoke access confirmation dialog"
38. **text** (#revoke_dialog_title) — label: "Revoke access?", content: "Revoke access?"
39. **text** (#revoke_dialog_body) — label: "This will immediately remove this app's access to your account data. You can rec", content: "This will immediately remove this app's access to your account data. You can rec"
40. **stack** (#revoke_dialog_actions) — label: "Revoke dialog action buttons"
41. **button** (#revoke_dialog_cancel_button) — label: "Cancel"
42. **button** (#revoke_dialog_confirm_button) — label: "Revoke"
43. **image** (#empty_state_icon) — label: "No connected apps illustration", content: "ic_link_off"
44. **text** (#empty_state_title) — label: "No apps connected", content: "No apps connected"
45. **text** (#empty_state_body) — label: "Third-party apps you authorise will appear here. Visit your bank's app marketpla", content: "Third-party apps you authorise will appear here. Visit your bank's app marketpla"

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
