---
ui_yaml_sha: 960d425113a3a35aff29d013134c27c798bd3bf3da5674a68138bf31e49ec445
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 15b16b9de6ac9449e7e4952399d0d9b39cd87f7774d015190c86fa3ff97494de

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: login
state: empty
state_visibility: empty

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# login — empty state

> Auto-generated from screens/login/ui.yaml @ SHA d1eb77e132c896ba
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: screen

## Layout
- type: scrollable_column
- padding: default
- alignment: start

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
11. **button** (#continue_hsbc_button) — label: "{strings.screen.login.cta.continue}", icon: "open_in_new"
12. **button** (#cancel_button) — label: "{strings.screen.login.cta.cancel}"
13. **empty_state** (#error_state) — "{strings.screen.login.error.title}"
   - **button** (#retry_button) — label: "{strings.screen.login.error.retry}"
14. **empty_state** (#login_empty_state) — "{strings.screen.login.empty.title}"
   - **button** (#login_empty_back_button) — label: "{strings.screen.login.empty.go_back}"

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
