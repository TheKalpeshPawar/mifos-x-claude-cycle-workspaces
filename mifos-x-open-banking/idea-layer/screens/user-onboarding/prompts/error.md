---
ui_yaml_sha: db26dc91d078de94511b20fba1941fc55412b0d42710df52771781ccac03cc24
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 33070a2fed5fe4d8421375496405959c8b83b680af79cc8ce6711437176c8b16

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: user-onboarding
state: error
state_visibility: error

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# user-onboarding — error state

> Auto-generated from screens/user-onboarding/ui.yaml @ SHA f6c618b0fa05ae37
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: screen

## Layout
- type: scrollable_column
- padding: default
- alignment: start

## Composition (top → bottom)
1. **progress_indicator** (#onboarding_loading_indicator)
2. **empty_state** (#onboarding_error_state) — "{strings.onboarding_error_title}"
   - **button** (#onboarding_error_retry_button) — label: "{strings.onboarding_error_retry}"
3. **empty_state** (#onboarding_empty_state) — "{strings.onboarding_empty_title}"
   - **button** (#onboarding_empty_skip_button) — label: "{strings.onboarding_empty_skip_button}"
4. **stepper** (#step_indicator_intro)
5. **image** (#hero_illustration)
6. **text** (#intro_headline)
7. **text** (#intro_body)
8. **chip** (#fapi_security_badge) — label: "{strings.onboarding_fapi_badge}", icon: "verified_user"
9. **chip** (#fca_regulated_badge) — label: "{strings.onboarding_fca_badge}", icon: "account_balance"
10. **button** (#intro_next_button) — label: "{strings.onboarding_intro_next}"
11. **stepper** (#step_indicator_permissions)
12. **section_header** (#what_we_read_header) — label: "{strings.onboarding_what_we_read}"
13. **list** (#permissions_list) — "permissions_list"
   - **list_item** (#perm_accounts) — icon: "manage_accounts"
   - **list_item** (#perm_balances) — icon: "account_balance"
   - **list_item** (#perm_transactions) — icon: "receipt_long"
   - **list_item** (#perm_standing_orders) — icon: "autorenew"
   - **list_item** (#perm_direct_debits) — icon: "subscriptions"
   - **list_item** (#perm_statements) — icon: "description"
14. **text** (#consent_duration_note)
15. **button** (#permissions_back_button) — label: "{strings.onboarding_step_back}"
16. **button** (#permissions_next_button) — label: "{strings.onboarding_step_next}"
17. **stepper** (#step_indicator_trust)
18. **section_header** (#what_we_never_do_header) — label: "{strings.onboarding_what_we_never_do}"
19. **list** (#reassurance_list) — "reassurance_list"
   - **list_item** (#never_payments) — icon: "money_off"
   - **list_item** (#never_password) — icon: "lock"
   - **list_item** (#never_locked_in) — icon: "cancel"
20. **divider** (#legal_divider)
21. **text** (#legal_footer)
22. **button** (#connect_hsbc_button) — label: "{strings.onboarding_connect_button}", icon: "open_in_new"
23. **button** (#trust_back_button) — label: "{strings.onboarding_step_back}"
24. **button** (#how_ob_works_button) — label: "{strings.onboarding_how_ob_works}"
25. **bottom_sheet** (#ob_explainer_sheet) — "ob_explainer_sheet"
   - **text** (#ob_explainer_title)
   - **list_item** (#ob_step1) — icon: "how_to_reg"
   - **list_item** (#ob_step2) — icon: "login"
   - **list_item** (#ob_step3) — icon: "shield"
   - **text** (#ob_explainer_revoke_note)
   - **button** (#ob_explainer_close_button) — label: "{strings.ob_explainer_close}"

## State-specific behavior
- Show an error illustration, a short message, and a single Retry action. No content rails visible.

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

- [ ] **Per-state shape:** the render shows ONLY this state ("error"). Do not blend multiple states into one mockup.
- [ ] **Real content:** every text label, image, and data point reflects the content source manifest above — no numbered generic items, no filler text, no dummy text, no empty strings.
- [ ] **Token fidelity:** colors come from the uploaded design system (primary/secondary/surface/etc.) by name; spacing comes from declared scale tokens. No invented hex codes, no invented size literals.
- [ ] **Component vocabulary:** every component in the render maps to a named design-system component (Card, FAB, BottomBar, etc.) — no invented or off-system components.
- [ ] **Archetype honored:** the layout follows the "screen" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
