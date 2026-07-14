---
ui_yaml_sha: 3eebe234cf8a7c3e289d140ce5ebbefa69fb582bb204292f60910f60a07cce72
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: b055f2b912a8b2ef091eeb916f21bbbd95a3fb9c88facdf3b6d19d30c6509e0a

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: transaction-detail
state: empty
state_visibility: empty

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# transaction-detail — empty state

> Auto-generated from screens/transaction-detail/ui.yaml @ SHA 0db6244a6c62fea2
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: screen

## Layout
- type: scrollable_column
- padding: default
- alignment: start

## Composition (top → bottom)
1. **progress_indicator**
2. **icon_button** (#back_button) — icon: "arrow_back"
3. **text** (#amount_header)
4. **text** (#transaction_currency_meta)
5. **text** (#merchant_name)
6. **chip** (#status_badge) — label: "{transaction.Status}"
7. **divider** (#header_separator)
8. **card** (#detail_card) — "detail_card"
   - **text** (#detail_card_header)
   - **list_item** (#booking_date_row) — label: "{strings.transaction_detail_booking_date}"
   - **divider**
   - **list_item** (#value_date_row) — label: "{strings.transaction_detail_value_date}"
   - **divider**
   - **list_item** (#category_row) — label: "{strings.transaction_detail_category}"
   - **divider**
   - **list_item** (#mcc_row) — label: "{strings.transaction_detail_mcc}"
   - **divider**
   - **list_item** (#balance_after_row) — label: "{strings.transaction_detail_balance_after}"
   - **divider**
   - **list_item** (#reference_row) — label: "{strings.transaction_detail_reference}"
   - **divider**
   - **list_item** (#bank_code_row) — label: "{strings.transaction_detail_bank_code}"
9. **empty_state** (#error_state) — "{strings.transaction_detail_error_title}"
   - **button** (#retry_button) — label: "{strings.transaction_detail_retry}"
   - **button** (#go_back_button) — label: "{strings.transaction_detail_go_back}"
10. **empty_state** (#transaction_empty_state) — "{strings.transaction_detail_empty_title}"
   - **button** (#transaction_empty_back_button) — label: "{strings.transaction_detail_go_back}"

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
- [ ] **Archetype honored:** the layout follows the "screen" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
