---
ui_yaml_sha: 30c96226cc2a33306019a30f631f69a8639af831639b60890e9f9811010161b4
design_md_hash: f734ecfba28b3b0688cbd7ca6f3d7fca27febb15fd021d72a4518ae0e3a4200d
app_shell_hash: 7b9c63f9aee4f5b5005b1d7533e7f5feab6427f398954987c34ee0f382b0ed69
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 2f9dc80eec2dd17a4de75668ed7e3b173de2894e4b6eba76da239a88021ca251

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: consent-list
state: empty
state_visibility: empty

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# consent-list — empty state

> Auto-generated from screens/consent-list/ui.yaml @ SHA e3194b591a103254
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
1. **progress_indicator**
2. **banner** (#reconfirm_banner) — title: "{strings.consent_list_reconfirm_banner_title}", icon: "warning_amber"
3. **text** (#active_section_label)
4. **list** (#active_consents_list) — "active_consents_list"
   - **card** (#consent_card) — "consent_card"
      - **row** (#consent_card_header_row) — "consent_card_header_row"
         - **image** (#bank_logo)
         - **chip** (#status_chip) — label: "{item.Data.Status}", icon: "{item.status_icon}"
      - **chip** (#reconfirm_urgency_chip) — label: "{strings.consent_list_reconfirm_chip}", icon: "warning_amber"
      - **text** (#permission_summary)
      - **text** (#expiry_countdown)
      - **text** (#granted_since)
5. **divider** (#section_divider)
6. **text** (#history_section_label)
7. **list** (#history_consents_list) — "history_consents_list"
   - **card** (#history_consent_card) — "history_consent_card"
      - **row** (#history_card_header_row) — "history_card_header_row"
         - **image** (#bank_logo_history)
         - **chip** (#history_status_chip) — label: "{item.Data.Status}", icon: "{item.status_icon}"
      - **text** (#history_expiry_label)
      - **text** (#history_connected_on)
8. **empty_state** (#empty_state) — "{strings.consent_list_empty_title}"
   - **button** (#connect_button) — label: "{strings.consent_list_connect}", on_click: { action: navigate_connect, target: user-onboarding }
9. **empty_state** (#error_state) — "{strings.consent_list_error_title}"
   - **button** (#retry_button) — label: "{strings.consent_list_retry}", on_click: { action: retry_load }
10. **empty_state** (#auth_error_state) — "{strings.consent_list_auth_error_title}"
   - **button** (#reauth_button) — label: "{strings.consent_list_reauth}", on_click: { action: navigate_reauth, target: login }

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
- [ ] **Archetype honored:** the layout follows the "index_list" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
