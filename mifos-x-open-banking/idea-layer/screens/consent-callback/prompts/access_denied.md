---
ui_yaml_sha: a5072ad7771938cebfbecdc81f55f9e9aeb1b3556f681cc1088c0f096deb6e87
design_md_hash: f734ecfba28b3b0688cbd7ca6f3d7fca27febb15fd021d72a4518ae0e3a4200d
app_shell_hash: 7b9c63f9aee4f5b5005b1d7533e7f5feab6427f398954987c34ee0f382b0ed69
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 8259b15a384dbac0755adb19356e4d22e4f2f6aab95af1df4bcbc8477f9f897f

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: consent-callback
state: access_denied
state_visibility: access_denied

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# consent-callback — access_denied state

> Auto-generated from screens/consent-callback/ui.yaml @ SHA 2706a048f4ec927a
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-feature-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

> DO NOT invent navigation, tabs, or screens beyond the declared app-shell (Home, Accounts, Pay, More) plus the composition below. Every nav item you render MUST come from that list.
> Only elements that navigate or perform an action may look tappable (cursor, ripple, pressed state). DO NOT add tap affordances to decorative content — page titles, section headings, avatars, standalone icons, badges, and static labels are NOT interactive.

## Archetype: empty_state

## Layout
- type: scrollable_column
- padding: default
- alignment: start
- responsive: any multi-column region MUST be mobile-first and collapse to a single column at narrow/phone widths — never a fixed multi-column grid with no single-column fallback.

## Composition (top → bottom)
1. **stack** (#loading_layout) — "loading_layout"
   - **progress_indicator** (#loading_spinner)
   - **spacer**
   - **text** (#loading_headline)
   - **spacer**
   - **text** (#loading_body)
2. **stack** (#success_layout) — "success_layout"
   - **icon** (#success_icon)
   - **spacer**
   - **text** (#success_headline)
   - **spacer**
   - **text** (#success_body)
3. **empty_state** (#awaiting_state) — "{strings.consent_callback_awaiting_title}"
   - **button** (#poll_again_button) — label: "{strings.consent_callback_poll_again}", on_click: { action: poll_consent_status }
4. **empty_state** (#error_state) — "{strings.consent_callback_error_title}"
   - **button** (#retry_button) — label: "{strings.consent_callback_retry}", on_click: { action: navigate_retry, target: login }
5. **empty_state** (#access_denied_state) — "{strings.consent_callback_denied_title}"
   - **button** (#denied_cta_button) — label: "{strings.consent_callback_denied_cta}", on_click: { action: navigate_retry, target: login }
6. **empty_state** (#security_error_state) — "{strings.consent_callback_security_error_title}"
   - **button** (#security_retry_button) — label: "{strings.consent_callback_security_cta}", on_click: { action: navigate_login, target: login }

## State-specific behavior
- Custom state "Access Denied" — render per the composition below.

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

- [ ] **Per-state shape:** the render shows ONLY this state ("access_denied"). Do not blend multiple states into one mockup.
- [ ] **Real content:** every text label, image, and data point reflects the content source manifest above — no numbered generic items, no filler text, no dummy text, no empty strings.
- [ ] **Token fidelity:** colors come from the uploaded design system (primary/secondary/surface/etc.) by name; spacing comes from declared scale tokens. No invented hex codes, no invented size literals.
- [ ] **Component vocabulary:** every component in the render maps to a named design-system component (Card, FAB, BottomBar, etc.) — no invented or off-system components.
- [ ] **Archetype honored:** the layout follows the "empty_state" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
