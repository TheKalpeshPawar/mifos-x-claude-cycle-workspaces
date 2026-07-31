---
ui_yaml_sha: dc2ab5eef0fa033108fd25974b00cf51ce36cd386fe8d5a2d65309aaa5ce11d4
design_md_hash: f734ecfba28b3b0688cbd7ca6f3d7fca27febb15fd021d72a4518ae0e3a4200d
app_shell_hash: 7b9c63f9aee4f5b5005b1d7533e7f5feab6427f398954987c34ee0f382b0ed69
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 2b909bdc189b957b0347e913db4e52a00fec03f749a02dc0fa5299d272abc0ab

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: direct-debits
state: loading
state_visibility: loading

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# direct-debits — loading state

> Auto-generated from screens/direct-debits/ui.yaml @ SHA 31dfcf7135e6a90d
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
1. **skeleton** (#loading_skeleton)
2. **icon_button** (#back_button) — icon: "arrow_back", on_click: { action: navigate_back, target: account-detail }
3. **chip_group** (#mandate_summary_chips)
4. **list** (#direct_debits_list) — "direct_debits_list"
   - **card** (#direct_debit_card) — "direct_debit_card"
      - **text** (#dd_originator_name)
      - **badge** (#dd_status_badge)
      - **text** (#dd_previous_amount)
      - **text** (#dd_previous_date)
      - **text** (#dd_mandate_id)
5. **empty_state** (#empty_direct_debits) — title: "{strings.direct_debits.empty_title}", icon: "subscriptions"
6. **empty_state** (#unsupported_direct_debits) — title: "{strings.direct_debits.unsupported_title}", icon: "info_outline"
7. **empty_state** (#error_state) — "{strings.direct_debits.error_title}"
   - **button** (#retry_button) — label: "{strings.direct_debits.retry_label}", on_click: { action: retryload }

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
- [ ] **Archetype honored:** the layout follows the "index_list" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
