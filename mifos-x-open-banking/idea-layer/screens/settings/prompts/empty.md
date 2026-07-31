---
ui_yaml_sha: fa85e05ffcdf0b3840573b6db5c5e062821b80c281a704578b9a7cf622526b00
design_md_hash: f734ecfba28b3b0688cbd7ca6f3d7fca27febb15fd021d72a4518ae0e3a4200d
app_shell_hash: 7b9c63f9aee4f5b5005b1d7533e7f5feab6427f398954987c34ee0f382b0ed69
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 6d3944e4719a12875a3502095cd799939c8699796ec9e429d5f60c5a77f7e4b6

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: settings
state: empty
state_visibility: empty

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# settings — empty state

> Auto-generated from screens/settings/ui.yaml @ SHA 6fe3677f197ff40e
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-feature-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

> DO NOT invent navigation, tabs, or screens beyond the declared app-shell (Home, Accounts, Pay, More) plus the composition below. Every nav item you render MUST come from that list.
> Only elements that navigate or perform an action may look tappable (cursor, ripple, pressed state). DO NOT add tap affordances to decorative content — page titles, section headings, avatars, standalone icons, badges, and static labels are NOT interactive.

## Archetype: settings

## Layout
- type: scrollable_column
- padding: default
- alignment: start
- responsive: any multi-column region MUST be mobile-first and collapse to a single column at narrow/phone widths — never a fixed multi-column grid with no single-column fallback.

## Composition (top → bottom)
1. **section_header** (#appearance_header) — label: "{strings.settings.section.appearance}"
2. **select** (#theme_row) — label: "{strings.settings.theme.label}", on_click: { action: togglethememenu }
3. **section_header** (#account_header) — label: "{strings.settings.section.account}"
4. **list_item** (#consents_row) — title: "{strings.settings.consents.title}", subtitle: "{strings.settings.consents.subtitle}", on_click: { action: navigate_consent_list, target: consent-list }
5. **section_header** (#about_header) — label: "{strings.settings.section.about_legal}"
6. **list_item** (#privacy_row) — title: "{strings.settings.privacy.title}", on_click: { action: open_privacy_url }
7. **list_item** (#licences_row) — title: "{strings.settings.licences.title}", on_click: { action: navigate_licences, target: licences }
8. **list_item** (#app_version_row) — title: "{strings.settings.app_version.title}", subtitle: "{appVersionLabel}"
9. **empty_state** (#settings_empty) — title: "{strings.settings.empty.title}"
10. **error_state** (#settings_error) — "{strings.settings.error.title}"
   - **button** (#retry_button) — label: "{strings.settings.error.retry}", on_click: { action: retryload }

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
- [ ] **Archetype honored:** the layout follows the "settings" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
