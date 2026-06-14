---
ui_yaml_sha: 003cc33aee7833db42dd545883d2c9a6b50587f4e66d99761203ccf500cd95b2
design_md_hash: 2b17083785e7e532a1554540e628db54640dfab77857b6c90d802767add94ba2
app_shell_hash: d2fe35b34f2ccfe703fcea97291ff9cb0453b148553d7b69b40f4cfa59d08766
design_read_hash: 60a4c95f7619b31daccc130861a96508d0cacf2f29734f43c35036c1f0280375
content_hash: 25a678d5d1616360160746372e2efb9f6b12f1717e7b0c50c58b18c21e9b703a

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: dashboard

feature: home
state: content
state_visibility: content

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# home — content state

> Auto-generated from screens/home/ui.yaml @ SHA 7a1de01dd030db0f
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: dashboard

## Layout
- type: scrollable_column
- padding: default
- alignment: start

## Composition (top → bottom)
1. **card** (#primary_account_card) — "primary_account_card"
   - **stack** (#hero_header_row) — "hero_header_row"
      - **stack** (#hero_greeting_col) — "hero_greeting_col"
         - **text** (#hero_greeting_line) — content: "Good morning"
         - **text** (#hero_greeting_name) — content: "Hello, Liam Carter"
         - **text** (#hero_greeting_date) — content: "Monday, 25 May 2026"
      - **box** (#hero_avatar) — "hero_avatar"
         - **text** (#hero_avatar_initials) — content: "LC"
   - **text** (#hero_account_label) — content: "Everyday Current"
   - **text** (#hero_account_identifier) — content: "GB29 NWBK 6016 1331 9268 19"
   - **text** (#hero_balance_label) — content: "Available Balance"
   - **text** (#hero_balance_amount) — content: "£4,250.00"
2. **text** (#services_section_title) — content: "Banking Services"
3. **stack** (#services_grid) — "services_grid"
   - **card** (#service_standing_orders) — "service_standing_orders"
      - **icon** (#service_standing_orders_icon) — content: "event_repeat"
      - **text** (#service_standing_orders_label) — content: "Standing Orders"
   - **card** (#service_business) — "service_business"
      - **icon** (#service_business_icon) — content: "storefront"
      - **text** (#service_business_label) — content: "Business"
   - **card** (#service_products) — "service_products"
      - **icon** (#service_products_icon) — content: "category"
      - **text** (#service_products_label) — content: "Products"
   - **card** (#service_find_atm) — "service_find_atm"
      - **icon** (#service_find_atm_icon) — content: "location_on"
      - **text** (#service_find_atm_label) — content: "Find ATM"
   - **card** (#service_insights) — "service_insights"
      - **icon** (#service_insights_icon) — content: "pie_chart"
      - **text** (#service_insights_label) — content: "Insights"
4. **dialog** (#account_picker_sheet) — "account_picker_sheet"
   - **text** (#account_picker_title) — content: "Choose default account"
   - **list_item** (#account_picker_row) — label: "Account option (one per account; check on the selected default)"
5. **spacer** (#bottom_spacer)

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
- [ ] **Archetype honored:** the layout follows the "dashboard" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
