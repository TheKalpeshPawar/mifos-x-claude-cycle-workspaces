---
ui_yaml_sha: 9b3d650e4f67967dbe434893324ed9f538a2f5c5f6c9e716d6b82939bbeb9b46
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: c19003479c7cafb975964bc9e2a4123621457b404714a911931b025d02c75d84

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: consent-detail
state: empty
state_visibility: empty

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# consent-detail — empty state

> Auto-generated from screens/consent-detail/ui.yaml @ SHA e3a290da5dc3daa6
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: screen

## Layout
- type: scrollable_column
- padding: default
- alignment: start

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
7. **button** (#reconfirm_button) — label: "{strings.consent_detail.reconfirm_button}", icon: "refresh"
8. **section_header** (#permissions_header) — label: "{strings.consent_detail.section.data_shared}"
9. **list** (#permissions_list) — "permissions_list"
   - **list_item** (#permission_row) — icon: "check_circle_outline"
10. **button** (#revoke_button) — label: "{strings.consent_detail.revoke_button}", icon: "link_off"
11. **dialog** (#revoke_confirm_dialog) — "{strings.consent_detail.revoke_dialog.title}"
   - **button** (#dialog_cancel_button) — label: "{strings.consent_detail.revoke_dialog.cancel}"
   - **button** (#dialog_confirm_button) — label: "{strings.consent_detail.revoke_dialog.confirm}"
12. **empty_state** (#error_state) — "{strings.consent_detail.error.title}"
   - **button** (#retry_button) — label: "{strings.consent_detail.error.retry}"
13. **empty_state** (#empty_state) — "{strings.consent_detail.empty.title}"
   - **button** (#empty_go_back_button) — label: "{strings.consent_detail.empty.go_back}"

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
