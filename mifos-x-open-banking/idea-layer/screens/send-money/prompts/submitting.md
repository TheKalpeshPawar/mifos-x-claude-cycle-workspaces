---
ui_yaml_sha: efa344738ce661263ac9a18f8138ede60254e9ff9f6ce532ed9e003c171afa0d
design_md_hash: f734ecfba28b3b0688cbd7ca6f3d7fca27febb15fd021d72a4518ae0e3a4200d
app_shell_hash: 7b9c63f9aee4f5b5005b1d7533e7f5feab6427f398954987c34ee0f382b0ed69
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 8edca0fc83bfdc662ee77c274a6b977b82bf8d3c95e004a62bfdef053714cc49

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: form

feature: send-money
state: submitting
state_visibility: submitting

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# send-money — submitting state

> Auto-generated from screens/send-money/ui.yaml @ SHA d24c528648bc2b81
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
1. **progress_indicator**
2. **step_indicator** (#form_step_indicator)
3. **list** (#debtor_account_selector) — "debtor_account_selector"
   - **list_item** (#debtor_account_row) — on_click: { action: select_debtor_account }
4. **list** (#creditor_selector) — "creditor_selector"
   - **list_item** (#creditor_row) — on_click: { action: select_creditor }
5. **empty_state** (#no_saved_payees) — title: "{strings.send_money.no_payees_title}", icon: "people_outline"
6. **button** (#manual_creditor_button) — label: "{strings.send_money.enter_manually}", on_click: { action: show_manual_creditor_entry }
7. **text_field** (#manual_sort_code) — label: "{strings.send_money.sort_code_label}"
8. **text_field** (#manual_account_number) — label: "{strings.send_money.account_number_label}"
9. **text_field** (#amount_field) — label: "{strings.send_money.amount_label}"
10. **text_field** (#reference_field) — label: "{strings.send_money.reference_label}"
11. **button** (#review_button) — label: "{strings.send_money.review_cta}", on_click: { action: review_payment }
12. **review_card** (#review_summary) — "review_summary"
   - **info_row** (#review_from_row) — label: "{strings.send_money.review_from_label}"
   - **info_row** (#review_to_row) — label: "{strings.send_money.review_to_label}"
   - **info_row** (#review_amount_row) — label: "{strings.send_money.review_amount_label}"
   - **info_row** (#review_reference_row) — label: "{strings.send_money.review_reference_label}"
13. **button** (#confirm_button) — label: "{strings.send_money.confirm_cta}", on_click: { action: confirm_and_stage_consent }
14. **button** (#cancel_button) — label: "{strings.send_money.cancel_cta}", on_click: { action: cancel_payment }
15. **progress_indicator** (#submitting_indicator)
16. **empty_state** (#payment_success) — "{strings.send_money.success_title}"
   - **button** (#view_payment_status_button) — label: "{strings.send_money.view_status_cta}", on_click: { action: navigate, target: payment-status }
17. **empty_state** (#error_state) — "{strings.send_money.error_title}"
   - **button** (#retry_button) — label: "{strings.send_money.retry}", on_click: { action: retry_submit }
   - **button** (#reauthorise_button) — label: "{strings.send_money.reauthorise}", on_click: { action: navigate, target: payment-consent }
   - **button** (#view_consents_button) — label: "{strings.send_money.view_consents}", on_click: { action: navigate, target: consent-list }
   - **button** (#edit_amount_button) — label: "{strings.send_money.edit_amount}", on_click: { action: back_step }

## State-specific behavior
- Custom state "Submitting" — render per the composition below.

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

- [ ] **Per-state shape:** the render shows ONLY this state ("submitting"). Do not blend multiple states into one mockup.
- [ ] **Real content:** every text label, image, and data point reflects the content source manifest above — no numbered generic items, no filler text, no dummy text, no empty strings.
- [ ] **Token fidelity:** colors come from the uploaded design system (primary/secondary/surface/etc.) by name; spacing comes from declared scale tokens. No invented hex codes, no invented size literals.
- [ ] **Component vocabulary:** every component in the render maps to a named design-system component (Card, FAB, BottomBar, etc.) — no invented or off-system components.
- [ ] **Archetype honored:** the layout follows the "form" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
