---
ui_yaml_sha: e38de56e4e0b3f94618e668bf709962d8777d5b3f2a96885ab2e0bfe4a406b07
design_md_hash: f734ecfba28b3b0688cbd7ca6f3d7fca27febb15fd021d72a4518ae0e3a4200d
app_shell_hash: 7b9c63f9aee4f5b5005b1d7533e7f5feab6427f398954987c34ee0f382b0ed69
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: dc79fb44c72770ea2bab58ecb1f80d788ee11b9ddb2e296553afdd34cdb0635c

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: login
state: empty
state_visibility: empty

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# login — empty state

> Auto-generated from screens/login/ui.yaml @ SHA bfc80202de4c1d8f
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-feature-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

> DO NOT invent navigation, tabs, or screens beyond the declared app-shell (Home, Accounts, Pay, More) plus the composition below. Every nav item you render MUST come from that list.
> Only elements that navigate or perform an action may look tappable (cursor, ripple, pressed state). DO NOT add tap affordances to decorative content — page titles, section headings, avatars, standalone icons, badges, and static labels are NOT interactive.

## Archetype: form

## Layout
- type: scrollable_column
- padding: default
- alignment: start
- responsive: any multi-column region MUST be mobile-first and collapse to a single column at narrow/phone widths — never a fixed multi-column grid with no single-column fallback.

## Composition (top → bottom)
1. **progress_indicator** (#loading_indicator)
2. **text** (#loading_label)
3. **progress_indicator** (#authorising_spinner)
4. **text** (#authorising_label)
5. **text** (#authorising_hint)
6. **card** (#hsbc_explainer_card) — "hsbc_explainer_card"
   - **image** (#hsbc_logo)
   - **text** (#ob_regulated_badge)
   - **text** (#explainer_headline)
   - **text** (#explainer_body)
   - **divider** (#card_divider)
   - **text** (#security_notice)
7. **section_header** (#permissions_header) — label: "{strings.screen.login.permissions.header}"
8. **list** (#permissions_list) — "permissions_list"
   - **list_item** (#permission_row) — icon: "check_circle_outline"
9. **text** (#consent_validity_note)
10. **text** (#consent_expiry_display)
11. **button** (#continue_hsbc_button) — label: "{strings.screen.login.cta.continue}", icon: "open_in_new", on_click: { action: start_oauth }
12. **button** (#cancel_button) — label: "{strings.screen.login.cta.cancel}", on_click: { action: navigate_back, target: user-onboarding }
13. **empty_state** (#error_state) — "{strings.screen.login.error.title}"
   - **button** (#retry_button) — label: "{strings.screen.login.error.retry}", on_click: { action: start_oauth }
14. **empty_state** (#login_empty_state) — "{strings.screen.login.empty.title}"
   - **button** (#login_empty_back_button) — label: "{strings.screen.login.empty.go_back}", on_click: { action: navigate_back, target: user-onboarding }

## State-specific behavior
- Show an empty-state illustration, a friendly message, and one primary call-to-action button.

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

- [ ] **Per-state shape:** the render shows ONLY this state ("empty"). Do not blend multiple states into one mockup.
- [ ] **Real content:** every text label, image, and data point reflects the content source manifest above — no numbered generic items, no filler text, no dummy text, no empty strings.
- [ ] **Token fidelity:** colors come from the uploaded design system (primary/secondary/surface/etc.) by name; spacing comes from declared scale tokens. No invented hex codes, no invented size literals.
- [ ] **Component vocabulary:** every component in the render maps to a named design-system component (Card, FAB, BottomBar, etc.) — no invented or off-system components.
- [ ] **Archetype honored:** the layout follows the "form" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
