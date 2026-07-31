---
ui_yaml_sha: b6bb85d0ec326fe2fc5ef53e31ad0097f819b751795d46a0557c9281c1650c22
design_md_hash: f734ecfba28b3b0688cbd7ca6f3d7fca27febb15fd021d72a4518ae0e3a4200d
app_shell_hash: 7b9c63f9aee4f5b5005b1d7533e7f5feab6427f398954987c34ee0f382b0ed69
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 2b16c9c4b4f8aa2100b32b176d1bbb73b9cb002e0e2fb2efda22a411c38b2fb5

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: consent-detail
state: empty
state_visibility: empty

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# consent-detail — empty state

> Auto-generated from screens/consent-detail/ui.yaml @ SHA 2a9fb13874db3915
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-feature-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

> DO NOT invent navigation, tabs, or screens beyond the declared app-shell (Home, Accounts, Pay, More) plus the composition below. Every nav item you render MUST come from that list.
> Only elements that navigate or perform an action may look tappable (cursor, ripple, pressed state). DO NOT add tap affordances to decorative content — page titles, section headings, avatars, standalone icons, badges, and static labels are NOT interactive.

## Archetype: detail_screen

## Layout
- type: scrollable_column
- padding: default
- alignment: start
- responsive: any multi-column region MUST be mobile-first and collapse to a single column at narrow/phone widths — never a fixed multi-column grid with no single-column fallback.

## Composition (top → bottom)
1. **progress_indicator** (#load_progress)
2. **progress_indicator** (#revoke_progress) — label: "{strings.consent_detail.revoking_label}"
3. **card** (#status_header_card) — "status_header_card"
   - **row** (#bank_identity_row) — "bank_identity_row"
      - **image** (#bank_logo)
      - **chip** (#status_chip) — label: "{consent.Data.Status}", icon: "check_circle"
   - **text** (#consent_id_label)
4. **card** (#expiry_warning_banner) — "expiry_warning_banner"
   - **row** (#expiry_warning_row) — "expiry_warning_row"
      - **icon** (#expiry_warning_icon)
      - **text** (#expiry_warning_text)
5. **section_header** (#dates_header) — label: "{strings.consent_detail.section.access_period}"
6. **list** (#dates_list) — "dates_list"
   - **list_item** (#created_date_row) — icon: "event"
   - **list_item** (#expiry_date_row) — icon: "event_busy"
   - **list_item** (#transaction_from_row) — icon: "history"
   - **list_item** (#transaction_to_row) — icon: "event_available"
7. **button** (#reconfirm_button) — label: "{strings.consent_detail.reconfirm_button}", icon: "refresh", on_click: { action: navigate_reconfirm, target: login }
8. **section_header** (#permissions_header) — label: "{strings.consent_detail.section.data_shared}"
9. **list** (#permissions_list) — "permissions_list"
   - **list_item** (#permission_row) — icon: "check_circle_outline"
10. **button** (#revoke_button) — label: "{strings.consent_detail.revoke_button}", icon: "link_off", on_click: { action: confirm_revoke }
11. **dialog** (#revoke_confirm_dialog) — "{strings.consent_detail.revoke_dialog.title}"
   - **button** (#dialog_cancel_button) — label: "{strings.consent_detail.revoke_dialog.cancel}", on_click: { action: dismiss_revoke_confirm }
   - **button** (#dialog_confirm_button) — label: "{strings.consent_detail.revoke_dialog.confirm}", on_click: { action: execute_revoke }
12. **empty_state** (#error_state) — "{strings.consent_detail.error.title}"
   - **button** (#retry_button) — label: "{strings.consent_detail.error.retry}", on_click: { action: retry_load }
13. **empty_state** (#empty_state) — "{strings.consent_detail.empty.title}"
   - **button** (#empty_go_back_button) — label: "{strings.consent_detail.empty.go_back}", on_click: { action: navigate_back, target: consent-list }

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
- [ ] **Archetype honored:** the layout follows the "detail_screen" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
