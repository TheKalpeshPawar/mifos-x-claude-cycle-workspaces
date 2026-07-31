---
ui_yaml_sha: 329f9c2dc1074f6f06f593a9cf08a029c6360a039c605e52d066d9f2ff287e39
design_md_hash: f734ecfba28b3b0688cbd7ca6f3d7fca27febb15fd021d72a4518ae0e3a4200d
app_shell_hash: 7b9c63f9aee4f5b5005b1d7533e7f5feab6427f398954987c34ee0f382b0ed69
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: f9fbcc6b8196f9a81c625c25e126a6412b5b3ea0cd718091b9fa20297f8eb4e5

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: detail_screen

feature: statement-detail
state: content
state_visibility: content

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# statement-detail — content state

> Auto-generated from screens/statement-detail/ui.yaml @ SHA 1de02e50665a3b82
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
1. **progress_indicator**
2. **card** (#statement_header_card) — "statement_header_card"
   - **text** (#statement_reference)
   - **text** (#statement_period)
   - **text** (#statement_type)
   - **text** (#statement_created)
3. **section_header** (#balances_header) — label: "{strings.stmt_detail.section.balances}"
4. **list** (#balances_list) — "balances_list"
   - **list_item** (#balance_row) — 6 items: "40051512345678", "40051512345678", "40051512345678", "40051512345678", "40051512345678", "40051512345678"
5. **section_header** (#fees_header) — label: "{strings.stmt_detail.section.fees}"
6. **list** (#fees_list) — "fees_list"
   - **list_item** (#fee_row) — 6 items: "40051512345678", "40051512345678", "40051512345678", "40051512345678", "40051512345678", "40051512345678"
7. **section_header** (#interest_header) — label: "{strings.stmt_detail.section.interest}"
8. **list** (#interest_list) — "interest_list"
   - **list_item** (#interest_row) — 6 items: "40051512345678", "40051512345678", "40051512345678", "40051512345678", "40051512345678", "40051512345678"
9. **section_header** (#transactions_header) — 6 items: "40051512345678", "40051512345678", "40051512345678", "40051512345678", "40051512345678", "40051512345678"
10. **list** (#statement_txns_list) — "statement_txns_list"
   - **list_item** (#statement_txn_row) — 6 items: "40051512345678", "40051512345678", "40051512345678", "40051512345678", "40051512345678", "40051512345678"
11. **empty_state** (#empty_txns_state) — title: "{strings.stmt_detail.empty_txns.title}", icon: "receipt_long"
12. **button** (#download_pdf_button) — label: "{strings.stmt_detail.action.download_pdf}", icon: "download", on_click: { action: download_statement_pdf }
13. **progress_indicator** (#download_progress)
14. **snackbar** (#download_result_snackbar)
15. **empty_state** (#error_state) — "{strings.stmt_detail.error.title}"
   - **button** (#retry_button) — label: "{strings.stmt_detail.action.retry}", on_click: { action: retry_load }

## State-specific behavior
- Fully populated with the real demo content listed below.

## Content source manifest
- demo-data.statementTransactions[0..5]
- demo-data.statementTransactions[0..5]
- demo-data.statementTransactions[0..5]
- demo-data.statementTransactions[0..5]
- demo-data.statementTransactions[0..5]

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

- [ ] **Per-state shape:** the render shows ONLY this state ("content"). Do not blend multiple states into one mockup.
- [ ] **Real content:** every text label, image, and data point reflects the content source manifest above — no numbered generic items, no filler text, no dummy text, no empty strings.
- [ ] **Token fidelity:** colors come from the uploaded design system (primary/secondary/surface/etc.) by name; spacing comes from declared scale tokens. No invented hex codes, no invented size literals.
- [ ] **Component vocabulary:** every component in the render maps to a named design-system component (Card, FAB, BottomBar, etc.) — no invented or off-system components.
- [ ] **Archetype honored:** the layout follows the "detail_screen" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
