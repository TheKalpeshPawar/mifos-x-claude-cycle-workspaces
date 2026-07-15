---
ui_yaml_sha: 5ce0e5b710baab509a003bdb8fa35a50b068c97218447942a71954c569cb3847
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 4720c5bba86c016b460a1a66553a9d7332d1cff2037b1e2446de945652c60c0a

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: settings

feature: settings
state: clear_confirm
state_visibility: clear_confirm

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# settings — clear_confirm state

> Auto-generated from screens/settings/ui.yaml @ SHA bf3139ec90afe263
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: settings

## Layout
- type: scrollable_column
- padding: default
- alignment: start

## Composition (top → bottom)
1. **skeleton** (#settings_loading_skeleton)
2. **section_header** (#appearance_header) — label: "{strings.settings.section.appearance}"
3. **list** (#appearance_list) — "appearance_list"
   - **list_item** (#theme_row) — label: "{strings.settings.theme.label}"
4. **section_header** (#security_header) — label: "{strings.settings.section.security}"
5. **list** (#security_list) — "security_list"
   - **list_item** (#biometric_row) — label: "{strings.settings.biometric_lock.label}"
   - **list_item** (#session_timeout_row) — label: "{strings.settings.session_timeout.label}"
6. **section_header** (#permissions_header) — label: "{strings.settings.section.permissions}"
7. **list** (#permissions_list) — "permissions_list"
   - **info_row** (#location_permission_row) — label: "{strings.settings.permissions.location}", icon: "location_on"
8. **section_header** (#notifications_header) — label: "{strings.settings.section.notifications}"
9. **list** (#notifications_list) — "notifications_list"
   - **list_item** (#consent_expiry_notif_row) — label: "{strings.settings.consent_expiry_notif.label}"
   - **list_item** (#security_alerts_notif_row) — label: "{strings.settings.security_alerts_notif.label}"
10. **section_header** (#storage_header) — label: "{strings.settings.section.storage}"
11. **list** (#storage_list) — "storage_list"
   - **info_row** (#pfm_storage_location_row) — label: "{strings.settings.storage.pfm_data}", icon: "storage"
   - **list_item** (#clear_pfm_cache_row) — label: "{strings.settings.storage.clear_pfm_cache}", icon: "cleaning_services"
12. **section_header** (#account_header) — label: "{strings.settings.section.account}"
13. **list** (#account_links_list) — "account_links_list"
   - **list_item** (#manage_consents_row) — label: "{strings.settings.manage_consents.label}", icon: "policy"
   - **list_item** (#profile_row) — label: "{strings.settings.profile.label}", icon: "account_circle"
   - **list_item** (#clear_local_data_row) — label: "{strings.settings.clear_local_data.label}", icon: "delete_sweep"
14. **section_header** (#about_header) — label: "{strings.settings.section.about_legal}"
15. **list** (#about_list) — "about_list"
   - **list_item** (#terms_row) — label: "{strings.settings.terms.label}", icon: "article"
   - **list_item** (#privacy_row) — label: "{strings.settings.privacy.label}", icon: "privacy_tip"
   - **list_item** (#licences_row) — label: "{strings.settings.licences.label}", icon: "info_outline"
   - **list_item** (#app_version_row) — label: "{strings.settings.app_version.label}"
16. **bottom_sheet** (#clear_local_data_sheet) — "{strings.settings.clear_local_data.dialog_title}"
   - **button** (#cancel_clear_local_data_button) — label: "{strings.settings.clear_local_data.dialog_cancel}"
   - **button** (#confirm_clear_local_data_button) — label: "{strings.settings.clear_local_data.dialog_confirm}"
17. **empty_state** (#settings_empty_state) — title: "{strings.settings.empty.title}", icon: "settings"
18. **empty_state** (#settings_error_state) — "{strings.settings.error.title}"
   - **button** (#settings_error_retry_button) — label: "{strings.settings.error.retry}"

## State-specific behavior
- Custom state "Clear Confirm" — render per the composition below.

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

- [ ] **Per-state shape:** the render shows ONLY this state ("clear_confirm"). Do not blend multiple states into one mockup.
- [ ] **Real content:** every text label, image, and data point reflects the content source manifest above — no numbered generic items, no filler text, no dummy text, no empty strings.
- [ ] **Token fidelity:** colors come from the uploaded design system (primary/secondary/surface/etc.) by name; spacing comes from declared scale tokens. No invented hex codes, no invented size literals.
- [ ] **Component vocabulary:** every component in the render maps to a named design-system component (Card, FAB, BottomBar, etc.) — no invented or off-system components.
- [ ] **Archetype honored:** the layout follows the "settings" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
