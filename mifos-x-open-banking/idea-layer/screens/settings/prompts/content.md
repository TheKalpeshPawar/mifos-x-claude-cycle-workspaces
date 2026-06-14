---
ui_yaml_sha: ae707f738eeb02e32825f7becefa1bb47fafdea1a5ac94109454ecc6fa260b88
design_md_hash: 2b17083785e7e532a1554540e628db54640dfab77857b6c90d802767add94ba2
app_shell_hash: d2fe35b34f2ccfe703fcea97291ff9cb0453b148553d7b69b40f4cfa59d08766
design_read_hash: 60a4c95f7619b31daccc130861a96508d0cacf2f29734f43c35036c1f0280375
content_hash: 2b57d79d1607238ebe385914e9e097964370f4930e447ee8a9a2e2e40446dd35

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: settings

feature: settings
state: content
state_visibility: content

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# settings — content state

> Auto-generated from screens/settings/ui.yaml @ SHA 3094caf56fcb3dd0
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: settings

## Layout
- type: column
- padding: spacing.lg
- alignment: start

## Composition (top → bottom)
1. **stack** (#settings_root)
2. **card** (#settings_profile_header_card)
3. **box** (#settings_profile_initials) — content: "M"
4. **text** (#settings_profile_name) — content: "Mifos User"
5. **text** (#settings_profile_email) — content: "user@example.com"
6. **text** (#settings_appearance_header) — content: "Appearance"
7. **card** (#settings_appearance_group)
8. **stack** (#settings_theme_follow_system_row)
9. **text** (#settings_theme_follow_system_label) — content: "Follow System"
10. **input** (#settings_theme_follow_system_toggle) — label: "Follow System"
11. **divider** (#settings_divider_theme_1)
12. **stack** (#settings_theme_light_row)
13. **text** (#settings_theme_light_label) — content: "Light Mode"
14. **input** (#settings_theme_light_toggle) — label: "Light Mode"
15. **divider** (#settings_divider_theme_2)
16. **stack** (#settings_theme_dark_row)
17. **text** (#settings_theme_dark_label) — content: "Dark Mode"
18. **input** (#settings_theme_dark_toggle) — label: "Dark Mode"
19. **divider** (#settings_divider_appearance)
20. **stack** (#settings_language_row)
21. **text** (#settings_language_label) — content: "Language"
22. **input** (#settings_language_select) — label: "Language"
23. **text** (#settings_security_header) — content: "Security"
24. **card** (#settings_security_group)
25. **stack** (#settings_biometric_row)
26. **text** (#settings_biometric_label) — content: "Biometric Login"
27. **input** (#settings_biometric_toggle) — label: "Biometric Login"
28. **divider** (#settings_divider_security)
29. **stack** (#settings_reset_password_row)
30. **text** (#settings_reset_password_label) — content: "Reset Password"
31. **icon** (#settings_reset_password_chevron) — content: "chevron_right"
32. **dialog** (#settings_reset_password_dialog)
33. **text** (#settings_reset_password_dialog_body) — content: "We'll email a password reset link to your registered address."
34. **button** (#settings_reset_password_dialog_confirm) — label: "Send link"
35. **button** (#settings_reset_password_dialog_cancel) — label: "Cancel"
36. **dialog** (#settings_reset_message_dialog)
37. **text** (#settings_reset_message_body) — content: "If your account is valid, a password reset link has been emailed to you."
38. **button** (#settings_reset_message_ok) — label: "OK"
39. **card** (#settings_data_consent_card)
40. **icon** (#settings_data_consent_icon) — content: "shield"
41. **text** (#settings_data_consent_label) — content: "Data & Consent"
42. **text** (#settings_data_consent_subtitle) — content: "Review and revoke account access you've granted"
43. **text** (#settings_about_header) — content: "About"
44. **card** (#settings_about_about_card)
45. **icon** (#settings_about_about_icon) — content: "info"
46. **text** (#settings_about_about_label) — content: "About Mifos X Open Banking"
47. **card** (#settings_about_terms_card)
48. **icon** (#settings_about_terms_icon) — content: "article"
49. **text** (#settings_about_terms_label) — content: "Terms of Service"
50. **card** (#settings_about_privacy_card)
51. **icon** (#settings_about_privacy_icon) — content: "privacy_tip"
52. **text** (#settings_about_privacy_label) — content: "Privacy Policy"
53. **card** (#settings_about_licenses_card)
54. **icon** (#settings_about_licenses_icon) — content: "gavel"
55. **text** (#settings_about_licenses_label) — content: "Open-source Licences"
56. **button** (#settings_sign_out_button) — label: "Sign out"
57. **text** (#settings_footer) — content: "Mifos X Open Banking  ·  v1.0.0"

## State-specific behavior
- Fully populated with the real demo content listed below.

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

- [ ] **Per-state shape:** the render shows ONLY this state ("content"). Do not blend multiple states into one mockup.
- [ ] **Real content:** every text label, image, and data point reflects the content source manifest above — no numbered generic items, no filler text, no dummy text, no empty strings.
- [ ] **Token fidelity:** colors come from the uploaded design system (primary/secondary/surface/etc.) by name; spacing comes from declared scale tokens. No invented hex codes, no invented size literals.
- [ ] **Component vocabulary:** every component in the render maps to a named design-system component (Card, FAB, BottomBar, etc.) — no invented or off-system components.
- [ ] **Archetype honored:** the layout follows the "settings" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
