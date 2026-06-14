---
ui_yaml_sha: c914a33e7bebf707b3d60663987107732c5e4db0741f63e5759a4e30102e3c92
design_md_hash: 2b17083785e7e532a1554540e628db54640dfab77857b6c90d802767add94ba2
app_shell_hash: d2fe35b34f2ccfe703fcea97291ff9cb0453b148553d7b69b40f4cfa59d08766
design_read_hash: 60a4c95f7619b31daccc130861a96508d0cacf2f29734f43c35036c1f0280375
content_hash: 8788a4804e75b250d7971d77e71e1066900bf984f5713c79a885b8fc4af87722

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: index_list

feature: accounts
state: no_network
state_visibility: no_network

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# accounts — no_network state

> Auto-generated from screens/accounts/ui.yaml @ SHA 949a758a51b8761c
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: index_list

## Layout
- type: scrollable_column
- padding: default
- alignment: start

## Composition (top → bottom)
1. **stack** (#accounts_header) — "accounts_header"
   - **text** (#accounts_title) — content: "My Accounts"
   - **icon** (#accounts_help_icon) — content: "help_outline"
2. **text_field** (#accounts_search)
3. **stack** (#bank_group_1_header) — "bank_group_1_header"
   - **stack** (#bank_group_1_title_row) — "bank_group_1_title_row"
      - **icon** (#bank_group_1_icon) — content: "account_balance"
      - **stack** (#bank_group_1_title_col) — "bank_group_1_title_col"
         - **text** (#bank_group_1_name) — content: "Mifos Bank UK"
         - **text** (#bank_group_1_count) — content: "2 accounts"
4. **box** (#account_card_1) — "account_card_1"
   - **stack** (#acct1_header_row) — "acct1_header_row"
      - **text** (#acct1_label) — content: "Primary Checking"
      - **box** (#acct1_type_badge) — "acct1_type_badge"
         - **text** (#acct1_type_label) — content: "CHECKING"
   - **text** (#acct1_balance) — content: "£4,250.00"
   - **stack** (#acct1_iban_row) — "acct1_iban_row"
      - **icon** (#acct1_iban_icon) — content: "account_box"
      - **text** (#acct1_iban) — content: "DE89 3704 0044 0532 0130 00"
5. **box** (#account_card_2) — "account_card_2"
   - **stack** (#acct2_header_row) — "acct2_header_row"
      - **text** (#acct2_label) — content: "Holiday Savings"
      - **box** (#acct2_type_badge) — "acct2_type_badge"
         - **text** (#acct2_type_label) — content: "SAVINGS"
   - **text** (#acct2_balance) — content: "£6,180.50"
   - **stack** (#acct2_iban_row) — "acct2_iban_row"
      - **icon** (#acct2_iban_icon) — content: "account_box"
      - **text** (#acct2_iban) — content: "DE89 3704 0044 0532 0131 00"
6. **stack** (#bank_group_2_header) — "bank_group_2_header"
   - **stack** (#bank_group_2_title_row) — "bank_group_2_title_row"
      - **icon** (#bank_group_2_icon) — content: "account_balance"
      - **stack** (#bank_group_2_title_col) — "bank_group_2_title_col"
         - **text** (#bank_group_2_name) — content: "Mifos Business UK"
         - **text** (#bank_group_2_count) — content: "1 account"
7. **box** (#account_card_3) — "account_card_3"
   - **stack** (#acct3_header_row) — "acct3_header_row"
      - **text** (#acct3_label) — content: "Business Current"
      - **box** (#acct3_type_badge) — "acct3_type_badge"
         - **text** (#acct3_type_label) — content: "BUSINESS"
   - **text** (#acct3_balance) — content: "£2,050.00"
   - **stack** (#acct3_iban_row) — "acct3_iban_row"
      - **icon** (#acct3_iban_icon) — content: "account_box"
      - **text** (#acct3_iban) — content: "DE89 3704 0044 0532 0132 00"
8. **text** (#accounts_no_match_row) — content: "No accounts match your search."

## State-specific behavior
- Custom state "No Network" — render per the composition below.

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

- [ ] **Per-state shape:** the render shows ONLY this state ("no_network"). Do not blend multiple states into one mockup.
- [ ] **Real content:** every text label, image, and data point reflects the content source manifest above — no numbered generic items, no filler text, no dummy text, no empty strings.
- [ ] **Token fidelity:** colors come from the uploaded design system (primary/secondary/surface/etc.) by name; spacing comes from declared scale tokens. No invented hex codes, no invented size literals.
- [ ] **Component vocabulary:** every component in the render maps to a named design-system component (Card, FAB, BottomBar, etc.) — no invented or off-system components.
- [ ] **Archetype honored:** the layout follows the "index_list" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
