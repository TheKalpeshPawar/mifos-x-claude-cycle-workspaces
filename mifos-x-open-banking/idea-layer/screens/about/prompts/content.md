---
ui_yaml_sha: 5a16d3154cc2a1398c7c465b589f6a3f16c37c495a1972c659feca46b38d7b31
design_md_hash: 2b17083785e7e532a1554540e628db54640dfab77857b6c90d802767add94ba2
app_shell_hash: d2fe35b34f2ccfe703fcea97291ff9cb0453b148553d7b69b40f4cfa59d08766
design_read_hash: 60a4c95f7619b31daccc130861a96508d0cacf2f29734f43c35036c1f0280375
content_hash: bcf12f6f8a845e25fe0ef71f095e700f30432ebac9a0b77b5439057a7f06716f

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: settings

feature: about
state: content
state_visibility: content

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# about — content state

> Auto-generated from screens/about/ui.yaml @ SHA e38c3bc7980dcde0
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: settings

## Layout
- type: column
- padding: spacing.lg
- alignment: start

## Composition (top → bottom)
1. **stack** (#about_root)
2. **stack** (#about_logo_section)
3. **image** (#about_logo_image) — label: "Mifos X logo", content: "account_balance"
4. **text** (#about_app_name_text) — content: "Mifos X Open Banking"
5. **text** (#about_tagline_text) — content: "Open Banking for Everyone"
6. **text** (#about_version_inline) — content: "Version 1.0.0"
7. **card** (#about_app_info_card)
8. **text** (#about_app_info_header) — content: "App"
9. **stack** (#about_version_row)
10. **text** (#about_version_label) — content: "Version"
11. **text** (#about_version_value) — content: "1.0.0"
12. **divider** (#about_divider_1)
13. **stack** (#about_license_row)
14. **text** (#about_license_label) — content: "License"
15. **text** (#about_license_value) — content: "MPL-2.0"
16. **divider** (#about_divider_2)
17. **stack** (#about_platform_row)
18. **text** (#about_platform_label) — content: "Platform"
19. **text** (#about_platform_value) — content: "Kotlin Multiplatform"
20. **card** (#about_project_card)
21. **text** (#about_project_header) — content: "About this app"
22. **text** (#about_project_body) — content: "Mifos X Open Banking is an open-source demonstration client for the Open Bank Pr"
23. **text** (#about_mifos_subheading) — content: "The Mifos Initiative"
24. **text** (#about_mifos_body) — content: "Built and maintained by the Mifos Initiative, a global community working to expa"
25. **text** (#about_obp_subheading) — content: "Open Bank Project sandbox"
26. **text** (#about_obp_body) — content: "All account, transaction, and counterparty data shown in this app comes from the"
27. **card** (#about_legal_card)
28. **text** (#about_legal_header) — content: "Legal & resources"
29. **stack** (#about_mifos_link_row)
30. **link** (#about_mifos_link) — label: "Mifos Initiative"
31. **icon** (#about_mifos_link_icon) — content: "open_in_new"
32. **divider** (#about_divider_3)
33. **stack** (#about_obp_link_row)
34. **link** (#about_obp_link) — label: "Open Bank Project"
35. **icon** (#about_obp_link_icon) — content: "open_in_new"
36. **divider** (#about_divider_4)
37. **stack** (#about_github_link_row)
38. **link** (#about_github_link) — label: "Source code on GitHub"
39. **icon** (#about_github_link_icon) — content: "open_in_new"
40. **divider** (#about_divider_5)
41. **stack** (#about_mpl_link_row)
42. **link** (#about_mpl_link) — label: "Mozilla Public License 2.0"
43. **icon** (#about_mpl_link_icon) — content: "open_in_new"
44. **text** (#about_attribution) — content: "Made with Kotlin Multiplatform and Compose Multiplatform by the Mifos community."

## State-specific behavior
- Fully populated with the real demo content listed below. This is the screen's initial state.

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
