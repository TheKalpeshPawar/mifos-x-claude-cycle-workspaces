---
ui_yaml_sha: b51d7921bf3928d3e13464667e49e127f505fd70a8a4bca78e7921a215462d7f
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 09282e79e7fc3cdbebaa96e07031a9e40738d18de28e34f5978518e66412ebc4

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: profile
state: empty
state_visibility: empty

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# profile — empty state

> Auto-generated from screens/profile/ui.yaml @ SHA 6d70dbe17b38aaab
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: screen

## Layout
- type: scrollable_column
- padding: default
- alignment: start

## Composition (top → bottom)
1. **progress_indicator**
2. **card** (#identity_header_card) — "identity_header_card"
   - **avatar** (#user_avatar)
   - **text** (#user_full_name)
   - **text** (#party_type)
3. **section_header** (#identity_section_header) — label: "{strings.profile_section_identity}"
4. **list** (#identity_list) — "identity_list"
   - **list_item** (#email_row) — label: "{strings.profile_identity_email_label}", icon: "email"
   - **list_item** (#mobile_row) — label: "{strings.profile_identity_mobile_label}", icon: "phone"
   - **list_item** (#address_row) — label: "{strings.profile_identity_address_label}", icon: "home"
5. **card** (#expiry_warning_banner) — "expiry_warning_banner"
   - **icon** (#warning_icon)
   - **text** (#expiry_warning_text)
   - **button** (#renew_consent_button) — label: "{strings.profile_button_renew_consent}"
6. **section_header** (#connection_section_header) — label: "{strings.profile_section_connection}"
7. **card** (#consent_summary_card) — "consent_summary_card"
   - **text** (#bank_label) — icon: "account_balance"
   - **list_item** (#consent_status_row) — label: "{strings.profile_connection_status_label}", icon: "verified"
   - **list_item** (#consent_expiry_row) — label: "{strings.profile_connection_expiry_label}", icon: "schedule"
   - **section_header** (#permissions_section_header) — label: "{strings.profile_connection_permissions_label}"
   - **list** (#permissions_list) — "permissions_list"
      - **list_item** (#perm_accounts_detail) — label: "{strings.perm_read_accounts_detail}", icon: "check_circle"
      - **list_item** (#perm_balances) — label: "{strings.perm_read_balances}", icon: "check_circle"
      - **list_item** (#perm_transactions) — label: "{strings.perm_read_transactions_detail}", icon: "check_circle"
      - **list_item** (#perm_party) — label: "{strings.perm_read_party}", icon: "check_circle"
   - **button** (#manage_consent_button) — label: "{strings.profile_button_manage_consent}"
8. **button** (#sign_out_button) — label: "{strings.profile_button_sign_out}"
9. **dialog** (#sign_out_dialog) — "{strings.profile_dialog_sign_out_title}"
   - **button** (#cancel_sign_out_button) — label: "{strings.profile_button_cancel}"
   - **button** (#confirm_sign_out_button) — label: "{strings.profile_button_sign_out}"
10. **empty_state** (#error_state) — "{strings.profile_error_title}"
   - **button** (#retry_button) — label: "{strings.profile_button_retry}"
11. **empty_state** (#profile_empty_state) — "{strings.profile_empty_title}"
   - **button** (#profile_empty_reauth_button) — label: "{strings.profile_empty_reauth}"

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
