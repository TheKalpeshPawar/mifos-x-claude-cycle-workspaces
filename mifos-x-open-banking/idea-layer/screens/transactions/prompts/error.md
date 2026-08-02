---
ui_yaml_sha: ef7c8e0cc5a6d0f922c8a0771858bde2c382ea9c7e20e39f062788f8afb9a9fa
design_md_hash: f734ecfba28b3b0688cbd7ca6f3d7fca27febb15fd021d72a4518ae0e3a4200d
app_shell_hash: 7b9c63f9aee4f5b5005b1d7533e7f5feab6427f398954987c34ee0f382b0ed69
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: c3c68d191c800375fcec46db94b38319c6685658310bd53a558437f3b6d266b0

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: transactions
state: error
state_visibility: error

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# transactions — error state

> Auto-generated from screens/transactions/ui.yaml @ SHA e8247dab87a36026
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-feature-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

> DO NOT invent navigation, tabs, or screens beyond the declared app-shell (Home, Accounts, Pay, More) plus the composition below. Every nav item you render MUST come from that list.
> Only elements that navigate or perform an action may look tappable (cursor, ripple, pressed state). DO NOT add tap affordances to decorative content — page titles, section headings, avatars, standalone icons, badges, and static labels are NOT interactive.

## Archetype: index_list

## Layout
- type: scrollable_column
- padding: default
- alignment: start
- responsive: any multi-column region MUST be mobile-first and collapse to a single column at narrow/phone widths — never a fixed multi-column grid with no single-column fallback.

## Composition (top → bottom)
1. **progress_indicator** (#loading_spinner)
2. **stat_block** (#period_summary)
3. **chip_row** (#filter_chips) — "filter_chips"
   - **chip** (#filter_all) — label: "{strings.transactions.filter.all}", on_click: { action: filter_transactions }
   - **chip** (#filter_money_in) — label: "{strings.transactions.filter.money_in}", icon: "arrow_downward", on_click: { action: filter_transactions }
   - **chip** (#filter_money_out) — label: "{strings.transactions.filter.money_out}", icon: "arrow_upward", on_click: { action: filter_transactions }
   - **chip** (#filter_date_range) — label: "{strings.transactions.filter.date_range}", icon: "date_range", on_click: { action: open_date_range_picker }
4. **search_bar** (#search_field) — label: "{strings.transactions.search.label}"
5. **list** (#transactions_list) — "transactions_list"
   - **section_header** (#date_group_header) — label: "{group.date}"
   - **list_item** (#transaction_row) — "transaction_row"
      - **text** (#tx_merchant)
      - **chip** (#tx_category_tag) — label: "{item.Category}"
      - **badge** (#tx_pending_badge) — label: "{strings.transactions.status.pending}"
6. **button** (#load_more_button) — label: "{strings.transactions.load_more}", on_click: { action: load_more_transactions }
7. **progress_indicator** (#pagination_loader)
8. **empty_state** (#empty_transactions) — "{strings.transactions.empty.title}"
   - **button** (#clear_filters_button) — label: "{strings.transactions.empty.clear_filters}", on_click: { action: clear_filters }
9. **empty_state** (#error_state) — "{strings.transactions.error.title}"
   - **button** (#retry_button) — label: "{strings.transactions.error.retry}", on_click: { action: retry_load }

## State-specific behavior
- Show an error illustration, a short message, and a single Retry action. No content rails visible.

## Content source manifest
- (no demo collections bound for this state)

## Components (vocabulary used in this prompt)
- (no named components extracted — see composition)

## Shell (app-shell resolved for this state)
- Home: navigates to home
- Accounts: navigates to accounts
- Pay: navigates to send-money
- More: navigates to settings
- Render MUST keep nav/bar elements consistent with the list above — present or absent, never partial.

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
- [ ] **Archetype honored:** the layout follows the "index_list" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
