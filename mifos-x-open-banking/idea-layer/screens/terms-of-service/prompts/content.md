---
ui_yaml_sha: 1e1b16e47d7afe21dce24d3a1edc5135c691830ef58591d08b2f44420514ef47
design_md_hash: 2b17083785e7e532a1554540e628db54640dfab77857b6c90d802767add94ba2
app_shell_hash: d2fe35b34f2ccfe703fcea97291ff9cb0453b148553d7b69b40f4cfa59d08766
design_read_hash: 60a4c95f7619b31daccc130861a96508d0cacf2f29734f43c35036c1f0280375
content_hash: 812ceaeb319071010d200f7603228475e821d89b2f1ff707a17fcfe52e83fe64

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: settings

feature: terms-of-service
state: content
state_visibility: content

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# terms-of-service — content state

> Auto-generated from screens/terms-of-service/ui.yaml @ SHA d202d5e43e86cd3f
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: settings

## Layout
- type: column
- padding: spacing.lg
- alignment: start

## Composition (top → bottom)
1. **stack** (#tos_root) — 1 items: "static_asset"
2. **card** (#tos_intro_card)
3. **text** (#tos_intro_header) — content: "Agreement Overview"
4. **text** (#tos_intro_body) — content: "These Terms of Service govern your use of Mifos X Open Banking, an open-source d"
5. **card** (#tos_acceptance_card)
6. **text** (#tos_acceptance_header) — content: "1. Acceptance of Terms"
7. **text** (#tos_acceptance_body) — content: "By installing the app, signing in with sandbox DirectLogin credentials, or other"
8. **card** (#tos_demo_service_card)
9. **text** (#tos_demo_service_header) — content: "2. A Demonstration Service, Not a Real Bank"
10. **text** (#tos_demo_service_body) — content: "Mifos X Open Banking is a demonstration application. It is not a bank, an e-mone"
11. **card** (#tos_account_usage_card)
12. **text** (#tos_account_usage_header) — content: "3. Accounts and Credentials"
13. **text** (#tos_account_usage_body) — content: "Access is provided through DirectLogin credentials issued for the Open Bank Proj"
14. **card** (#tos_prohibited_card)
15. **text** (#tos_prohibited_header) — content: "4. Acceptable Use"
16. **text** (#tos_prohibited_body) — content: "You agree not to: (a) attack, overload, or attempt to circumvent the security co"
17. **card** (#tos_licensing_card)
18. **text** (#tos_licensing_header) — content: "5. Open-Source Licensing and Intellectual Property"
19. **text** (#tos_licensing_body) — content: "The source code of Mifos X Open Banking is licensed under the Mozilla Public Lic"
20. **card** (#tos_data_handling_card)
21. **text** (#tos_data_handling_header) — content: "6. Sandbox Data"
22. **text** (#tos_data_handling_body) — content: "Anything you enter into the app is stored on the Open Bank Project sandbox and s"
23. **card** (#tos_warranty_card)
24. **text** (#tos_warranty_header) — content: "7. Disclaimer of Warranty"
25. **text** (#tos_warranty_body) — content: "The app and the sandbox services behind it are provided "as is" and "as availabl"
26. **card** (#tos_liability_card)
27. **text** (#tos_liability_header) — content: "8. Limitation of Liability"
28. **text** (#tos_liability_body) — content: "To the maximum extent permitted by applicable law, the Mifos Initiative, the pro"
29. **card** (#tos_changes_card)
30. **text** (#tos_changes_header) — content: "9. Changes to These Terms"
31. **text** (#tos_changes_body) — content: "These terms may be revised as the demonstration evolves. Material changes are an"
32. **card** (#tos_contact_card)
33. **text** (#tos_contact_header) — content: "10. Contact"
34. **text** (#tos_contact_body) — content: "Questions about these terms are welcome through the Mifos Initiative community a"
35. **text** (#tos_last_updated_text) — content: "Last updated: 28 May 2026 — Version 1.0"

## State-specific behavior
- Fully populated with the real demo content listed below. This is the screen's initial state.

## Content source manifest
- demo-data.demo_entries[0..0]

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
