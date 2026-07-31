---
ui_yaml_sha: 63022c4bdb68924065a26c8c126bffa4abfdb1db245af70354bf6aab55c6d4ba
design_md_hash: f734ecfba28b3b0688cbd7ca6f3d7fca27febb15fd021d72a4518ae0e3a4200d
app_shell_hash: 7b9c63f9aee4f5b5005b1d7533e7f5feab6427f398954987c34ee0f382b0ed69
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: d419e39cec0f255fea3c7ae06f94bc8349955eb9c40f4507951b008336b8b6bb

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: account-detail
state: loading
state_visibility: loading

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# account-detail — loading state

> Auto-generated from screens/account-detail/ui.yaml @ SHA ec8a89707d9483d1
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-feature-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

> DO NOT invent navigation, tabs, or screens beyond the declared app-shell (Home, Accounts, Pay, More) plus the composition below. Every nav item you render MUST come from that list.
> Only elements that navigate or perform an action may look tappable (cursor, ripple, pressed state). DO NOT add tap affordances to decorative content — page titles, section headings, avatars, standalone icons, badges, and static labels are NOT interactive.

## Archetype: detail_screen

## Layout
- type: scrollable_column
- padding: default
- alignment: start
- responsive: any multi-column region MUST be mobile-first and collapse to a single column at narrow/phone widths — never a fixed multi-column grid with no single-column fallback.

## Composition (top → bottom)
1. **progress_indicator** (#loading_spinner)
2. **icon_button** (#back_button) — icon: "arrow_back", on_click: { action: navigate_back, target: accounts }
3. **card** (#account_header_card) — "account_header_card"
   - **text** (#account_subtype_label)
   - **text** (#account_nickname)
   - **text** (#account_identification)
   - **text** (#account_currency)
   - **text** (#account_servicer)
   - **text** (#account_last_updated)
4. **card** (#open_banking_badge) — "open_banking_badge"
   - **text** (#open_banking_badge_text)
5. **section_header** (#balances_header) — label: "{strings.account_detail_section_balances}"
6. **list** (#balances_list) — "balances_list"
   - **list_item** (#balance_row)
7. **empty_state** (#balances_empty_state) — title: "{strings.account_detail_balances_empty_title}", icon: "account_balance_wallet"
8. **section_header** (#actions_header) — label: "{strings.account_detail_section_explore}"
9. **chip_row** (#action_chips) — "action_chips"
   - **chip** (#chip_transactions) — label: "{strings.nav_chip_transactions}", icon: "receipt_long", on_click: { action: navigate_transactions, target: transactions }
   - **chip** (#chip_statements) — label: "{strings.nav_chip_statements}", icon: "description", on_click: { action: navigate_statements, target: statements }
   - **chip** (#chip_standing_orders) — label: "{strings.nav_chip_standing_orders}", icon: "autorenew", on_click: { action: navigate_standing_orders, target: standing-orders }
   - **chip** (#chip_direct_debits) — label: "{strings.nav_chip_direct_debits}", icon: "subscriptions", on_click: { action: navigate_direct_debits, target: direct-debits }
   - **chip** (#chip_scheduled_payments) — label: "{strings.nav_chip_scheduled}", icon: "schedule", on_click: { action: navigate_scheduled_payments, target: scheduled-payments }
   - **chip** (#chip_beneficiaries) — label: "{strings.nav_chip_beneficiaries}", icon: "people", on_click: { action: navigate_beneficiaries, target: beneficiaries }
   - **chip** (#chip_atm_locator) — label: "{strings.account_detail.nav_chip_atm_label}", icon: "atm", on_click: { action: navigate_atm_locator, target: _placeholder-atm-locator }
   - **chip** (#chip_product) — label: "{strings.nav_chip_product}", icon: "description", on_click: { action: navigate_product, target: product }
   - **chip** (#chip_party) — label: "{strings.nav_chip_party}", icon: "person", on_click: { action: navigate_party, target: account-holder }
10. **empty_state** (#error_state) — "{strings.account_detail_error_title}"
   - **button** (#retry_button) — label: "{strings.account_detail_retry}", on_click: { action: retry_load }

## State-specific behavior
- Show shimmer/skeleton loaders matching the content layout block-for-block — no real text, no images. This is the screen's initial state.

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

- [ ] **Per-state shape:** the render shows ONLY this state ("loading"). Do not blend multiple states into one mockup.
- [ ] **Real content:** every text label, image, and data point reflects the content source manifest above — no numbered generic items, no filler text, no dummy text, no empty strings.
- [ ] **Token fidelity:** colors come from the uploaded design system (primary/secondary/surface/etc.) by name; spacing comes from declared scale tokens. No invented hex codes, no invented size literals.
- [ ] **Component vocabulary:** every component in the render maps to a named design-system component (Card, FAB, BottomBar, etc.) — no invented or off-system components.
- [ ] **Archetype honored:** the layout follows the "detail_screen" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
