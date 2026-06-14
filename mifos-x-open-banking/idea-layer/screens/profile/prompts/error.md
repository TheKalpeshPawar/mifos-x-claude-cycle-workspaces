---
ui_yaml_sha: 02cef7b3f1d2276eb0ff9e4668bc9e0c2b727b19f7d8d2b7b1d03a7c51ba4bfd
design_md_hash: 2b17083785e7e532a1554540e628db54640dfab77857b6c90d802767add94ba2
app_shell_hash: d2fe35b34f2ccfe703fcea97291ff9cb0453b148553d7b69b40f4cfa59d08766
design_read_hash: 60a4c95f7619b31daccc130861a96508d0cacf2f29734f43c35036c1f0280375
content_hash: a8a7695de10dac4df69a5bd2f9c79617987e57fe3a96f68b6bd46c7906759419

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: profile
state: error
state_visibility: error

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# profile — error state

> Auto-generated from screens/profile/ui.yaml @ SHA f6f44ded7b4e952f
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: profile

## Layout
- type: column
- padding: spacing.lg
- alignment: start

## Composition (top → bottom)
1. **stack** (#profile_root)
2. **stack** (#profile_avatar_section)
3. **box** (#profile_avatar_initials) — content: "MS"
4. **icon** (#profile_avatar_edit_icon) — content: "edit"
5. **text** (#profile_display_name) — content: "Maria Santos"
6. **stack** (#profile_form_section)
7. **text** (#profile_section_header) — content: "Personal Information"
8. **input** (#profile_full_name_field) — label: "Full Name"
9. **input** (#profile_email_field) — label: "Email Address"
10. **input** (#profile_phone_field) — label: "Phone Number"
11. **button** (#profile_change_password_button) — label: "Change Password"
12. **button** (#profile_logout_button) — label: "Log Out"
13. **icon** (#profile_error_icon) — content: "error_outline"
14. **text** (#profile_error_title) — content: "Could not load your profile"
15. **text** (#profile_error_body) — content: "Check your connection and try again."
16. **button** (#profile_error_retry_button) — label: "Retry"
17. **loading_indicator** (#profile_loading_spinner)

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
- [ ] **Archetype honored:** the layout follows the "profile" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
