---
ui_yaml_sha: 819802aefb153188857bd6e96b0b71603965ff0264b8a68176ac70aae0ca79b3
design_md_hash: 2b17083785e7e532a1554540e628db54640dfab77857b6c90d802767add94ba2
app_shell_hash: d2fe35b34f2ccfe703fcea97291ff9cb0453b148553d7b69b40f4cfa59d08766
design_read_hash: 60a4c95f7619b31daccc130861a96508d0cacf2f29734f43c35036c1f0280375
content_hash: 4edb4935cb4169e84cd2a027e25f01fa4dcabbeb0a15b5d4867ebc3b0845ca12

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: standing-orders
state: error
state_visibility: error

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# standing-orders — error state

> Auto-generated from screens/standing-orders/ui.yaml @ SHA 8b1b7c68a5976550
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: index_list

## Layout
- type: scrollable_column
- padding: default
- alignment: start

## Composition (top → bottom)
1. **card** (#account_selector) — label: "From account"
2. **text** (#account_selector_label) — label: "From account", content: "From account"
3. **text** (#account_selector_value) — label: "Selected account name", content: "Current Account"
4. **stack** (#title_count_row) — label: "Stats row"
5. **card** (#stat_active) — label: "ACTIVE stat"
6. **card** (#stat_monthly_total) — label: "MONTHLY TOTAL stat"
7. **card** (#stat_paused) — label: "PAUSED stat"
8. **chip_group** (#filter_chips) — label: "Status filter chips"
9. **list** (#orders_list) — label: "Standing orders list"
10. **card** (#order_card) — label: "Standing order card"
11. **text** (#order_name) — label: "Order name", content: "Standing order name"
12. **badge** (#order_status_badge) — label: "Status badge", content: "Active"
13. **text** (#order_counterparty) — label: "To counterparty", content: "To Landlord Holdings Ltd · Acc ••s001"
14. **text** (#order_from_account) — label: "From account line", content: "From Current Account"
15. **text** (#order_amount) — label: "Amount", content: "£1,200.00"
16. **text** (#order_frequency) — label: "Frequency", content: "Monthly"
17. **text** (#order_schedule_line) — label: "Schedule line", content: "Next: 1 Jun 2026"
18. **button** (#create_standing_order_fab) — label: "New order", content: "New order"
19. **dialog** (#no_payees_dialog) — title: "No payees", label: "No payees"
20. **empty_state** (#empty_state) — label: "No standing orders"
21. **error_state** (#error_state) — label: "Unable to load"

## State-specific behavior
- Show an error illustration, a short message, and a single Retry action. No content rails visible.

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

- [ ] **Per-state shape:** the render shows ONLY this state ("error"). Do not blend multiple states into one mockup.
- [ ] **Real content:** every text label, image, and data point reflects the content source manifest above — no numbered generic items, no filler text, no dummy text, no empty strings.
- [ ] **Token fidelity:** colors come from the uploaded design system (primary/secondary/surface/etc.) by name; spacing comes from declared scale tokens. No invented hex codes, no invented size literals.
- [ ] **Component vocabulary:** every component in the render maps to a named design-system component (Card, FAB, BottomBar, etc.) — no invented or off-system components.
- [ ] **Archetype honored:** the layout follows the "index_list" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
