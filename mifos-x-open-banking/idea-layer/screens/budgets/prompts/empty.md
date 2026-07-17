---
ui_yaml_sha: 9067dbba16d3f9ccbfdb74645bfaa2721e30c04046a18b92d1d0bdef2f0f8ce6
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 21a9d59161bfea49c6fc60e079c651988dd140902f99d749642878c570c1e57e

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: budgets
state: empty
state_visibility: empty

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# budgets — empty state

> Auto-generated from screens/budgets/ui.yaml @ SHA a6a8c359c017e34e
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

> DO NOT invent navigation, tabs, or screens beyond the declared app-shell (Home, Accounts, Transactions, More) plus the composition below. Every nav item you render MUST come from that list.
> Only elements that navigate or perform an action may look tappable (cursor, ripple, pressed state). DO NOT add tap affordances to decorative content — page titles, section headings, avatars, standalone icons, badges, and static labels are NOT interactive.

## Archetype: dashboard

## Layout
- type: scrollable_column
- padding: default
- alignment: start

## Composition (top → bottom)
1. **skeleton** (#budgets_skeleton)
2. **error_state** (#budgets_error) — "{strings.budgets.error_title}"
   - **button** (#retry_load_button) — label: "{strings.budgets.retry_button}", on_click: { action: retry_load }
3. **section_header** (#set_budget_header) — label: "{strings.budgets.set_budget_header}"
4. **card** (#set_budget_card) — "set_budget_card"
   - **select** (#budget_category_dropdown) — label: "{strings.budgets.category_label}", on_click: { action: select_budget_category }
   - **text_field** (#budget_amount_field) — label: "{strings.budgets.amount_label}", on_click: { action: update_budget_amount_field }
   - **button** (#save_budget_button) — label: "{strings.budgets.save_button}", on_click: { action: save_budget }
5. **text** (#budgets_storage_hint)
6. **section_header** (#budgets_header) — label: "{current_month_label}"
7. **list** (#budgets_list) — "budgets_list"
   - **card** (#budget_card) — "budget_card"
      - **list_item** (#budget_row_header) — label: "{item.category}"
      - **progress_linear** (#budget_progress_bar)
      - **text** (#over_budget_alert)
      - **row** (#budget_card_actions) — "budget_card_actions"
         - **button** (#view_category_spend_button) — label: "{strings.budgets.view_transactions}", on_click: { action: navigate_spending_by_category, target: spending-by-category }
         - **button** (#delete_budget_button) — label: "{strings.budgets.delete_button}", on_click: { action: delete_budget }
8. **empty_state** (#empty_state) — title: "{strings.budgets.empty_title}", icon: "savings"

## State-specific behavior
- Show an empty-state illustration, a friendly message, and one primary call-to-action button.

## Content source manifest
- (no demo collections bound for this state)

## Components (vocabulary used in this prompt)
- (no named components extracted — see composition)

## Shell (app-shell resolved for this state)
- Home: navigates to home
- Accounts: navigates to accounts
- Transactions: navigates to transactions
- More: navigates to settings
- Render MUST keep nav/bar elements consistent with the list above — present or absent, never partial.

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
