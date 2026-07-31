---
ui_yaml_sha: 5f67cd986e561fa6e8e9ae450fc70b8cd950abb5fd2f5d9ac89a377ee3ab1ed8
design_md_hash: f734ecfba28b3b0688cbd7ca6f3d7fca27febb15fd021d72a4518ae0e3a4200d
app_shell_hash: 7b9c63f9aee4f5b5005b1d7533e7f5feab6427f398954987c34ee0f382b0ed69
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 212a963a55536dfe6f20ec1a16417ca1490f0d830b92aa4c27382207204cb283

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: home
state: loading
state_visibility: loading

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# home — loading state

> Auto-generated from screens/home/ui.yaml @ SHA e0a9707c164ac3a4
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-feature-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

> DO NOT invent navigation, tabs, or screens beyond the declared app-shell (Home, Accounts, Pay, More) plus the composition below. Every nav item you render MUST come from that list.
> Only elements that navigate or perform an action may look tappable (cursor, ripple, pressed state). DO NOT add tap affordances to decorative content — page titles, section headings, avatars, standalone icons, badges, and static labels are NOT interactive.

## Archetype: dashboard

## Layout
- type: scrollable_column
- padding: default
- alignment: start
- responsive: any multi-column region MUST be mobile-first and collapse to a single column at narrow/phone widths — never a fixed multi-column grid with no single-column fallback.

## Composition (top → bottom)
1. **stack** (#loading_skeleton) — "loading_skeleton"
   - **shimmer** (#skeleton_hero)
   - **shimmer** (#skeleton_actions)
   - **shimmer** (#skeleton_tx_header)
   - **shimmer** (#skeleton_tx_1)
   - **shimmer** (#skeleton_tx_2)
   - **shimmer** (#skeleton_tx_3)
2. **bottom_sheet** (#account_selector_sheet) — "account_selector_sheet"
   - **list_item** (#account_selector_row) — on_click: { action: select_account }
3. **card** (#hero_balance_card) — "hero_balance_card"
   - **stack**
      - **stack**
         - **text** (#hero_account_subtype)
         - **icon** (#hero_account_icon)
      - **text** (#hero_nickname)
      - **text** (#hero_balance)
      - **stack**
         - **text** (#hero_available_label)
         - **text** (#hero_available_amount)
      - **text** (#hero_identification)
4. **stack** (#recent_transactions_section) — "recent_transactions_section"
   - **stack**
      - **section_header** (#recent_tx_header)
      - **text_button** (#view_all_transactions_link) — label: "{strings.home.recent_transactions.view_all}", on_click: { action: navigate_transactions, target: transactions }
   - **list** (#recent_transactions_list) — "recent_transactions_list"
      - **card** (#recent_tx_row) — "recent_tx_row"
         - **stack**
            - **icon** (#tx_category_icon)
            - **stack**
               - **text** (#tx_description)
               - **text** (#tx_date)
            - **text** (#tx_amount)
5. **empty_state** (#empty_home) — title: "{strings.home.empty.title}", icon: "account_balance_wallet"
6. **error_state** (#error_home) — "{strings.home.error.title}"
   - **button** (#retry_button) — label: "{strings.home.error.retry_button}", on_click: { action: retry_load }

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
- [ ] **Archetype honored:** the layout follows the "dashboard" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
