---
ui_yaml_sha: b38cee5db5f24f316125c385d229cf7d6339a4f0f8412d54914afdd6915de941
design_md_hash: 2b17083785e7e532a1554540e628db54640dfab77857b6c90d802767add94ba2
app_shell_hash: d2fe35b34f2ccfe703fcea97291ff9cb0453b148553d7b69b40f4cfa59d08766
design_read_hash: 60a4c95f7619b31daccc130861a96508d0cacf2f29734f43c35036c1f0280375
content_hash: 3816932c96060b47da695180d26e9d653b8277dabee6a6ee01117717eeff13ab

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: transaction-detail
state: empty
state_visibility: empty

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# transaction-detail — empty state

> Auto-generated from screens/transaction-detail/ui.yaml @ SHA 27d83b4014d7afe3
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: detail_screen

## Layout
- type: scrollable_column
- padding: default
- alignment: start

## Composition (top → bottom)
1. **box** (#amount_hero_section) — "amount_hero_section"
   - **text** (#amount_hero_value) — content: "-£42.50"
   - **stack** (#status_badge_row) — "status_badge_row"
      - **box** (#status_badge) — "status_badge"
         - **stack** (#status_badge_inner) — "status_badge_inner"
            - **icon** (#status_icon) — content: "check_circle"
            - **text** (#status_label) — content: "Completed"
2. **box** (#merchant_card) — "merchant_card"
   - **stack** (#merchant_row) — "merchant_row"
      - **image** (#merchant_logo) — content: "merchant_tesco_large"
      - **stack** (#merchant_info) — "merchant_info"
         - **text** (#merchant_name) — content: "Tesco Supermarket"
         - **box** (#category_badge) — "category_badge"
            - **text** (#category_label) — content: "Groceries"
3. **box** (#details_card) — "details_card"
   - **stack** (#detail_date_row) — "detail_date_row"
      - **text** (#detail_date_label) — content: "Date & Time"
      - **text** (#detail_date_value) — content: "25 May 2026, 14:32"
   - **divider** (#detail_div_1)
   - **stack** (#detail_reference_row) — "detail_reference_row"
      - **text** (#detail_reference_label) — content: "Reference"
      - **stack** (#reference_value_row) — "reference_value_row"
         - **text** (#detail_reference_value) — content: "SEPA-2026051500123"
         - **icon** (#copy_reference_icon) — content: "content_copy"
   - **divider** (#detail_div_2)
   - **stack** (#detail_type_row) — "detail_type_row"
      - **text** (#detail_type_label) — content: "Transaction Type"
      - **text** (#detail_type_value) — content: "SEPA Credit Transfer"
   - **divider** (#detail_div_3)
   - **stack** (#detail_from_row) — "detail_from_row"
      - **text** (#detail_from_label) — content: "From Account"
      - **stack** (#detail_from_value_col) — "detail_from_value_col"
         - **text** (#detail_from_account_name) — content: "Primary Checking"
         - **text** (#detail_from_iban) — content: "...0130"
   - **divider** (#detail_div_4)
   - **stack** (#detail_to_row) — "detail_to_row"
      - **text** (#detail_to_label) — content: "To"
      - **stack** (#detail_to_value_col) — "detail_to_value_col"
         - **text** (#detail_to_name) — content: "Tesco PLC"
         - **text** (#detail_to_iban) — content: "DE89 3704...0044"
4. **button** (#download_receipt_button) — label: "Download Receipt"
5. **stack** (#report_issue_row) — "report_issue_row"
   - **icon** (#report_issue_icon) — content: "flag"
   - **link** (#report_issue_link) — content: "Report an Issue"
6. **list_item** (#manage_tags_row)
7. **spacer** (#bottom_spacer)

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
- [ ] **Archetype honored:** the layout follows the "detail_screen" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
