---
ui_yaml_sha: 131a09e0d37fbc1576b279c79cba2fab14c487f4ebc9172bc37ef5cdf0a545bd
design_md_hash: 2b17083785e7e532a1554540e628db54640dfab77857b6c90d802767add94ba2
app_shell_hash: d2fe35b34f2ccfe703fcea97291ff9cb0453b148553d7b69b40f4cfa59d08766
design_read_hash: 60a4c95f7619b31daccc130861a96508d0cacf2f29734f43c35036c1f0280375
content_hash: 8c888896079512bc53e982b48f2ea1456be3a000c809e95fdea0f450ea3e2f1e

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: index_list

feature: beneficiaries
state: content
state_visibility: content

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# beneficiaries — content state

> Auto-generated from screens/beneficiaries/ui.yaml @ SHA 109f46107ad295f9
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: index_list

## Layout
- type: scrollable_column
- padding: default
- alignment: start

## Composition (top → bottom)
1. **card** (#beneficiary_account_selector) — label: "Beneficiaries of <account>", content: "Beneficiaries of <account>"
2. **input** (#beneficiary_search_bar) — label: "Search"
3. **text** (#recently_used_header) — label: "Recently Used", content: "Recently Used"
4. **card** (#recent_beneficiary_card) — label: "Recent beneficiary", content: "Recent beneficiary"
5. **divider** (#section_divider)
6. **stack** (#all_beneficiaries_header_row) — label: "All Beneficiaries"
7. **text** (#all_beneficiaries_header) — label: "All Beneficiaries", content: "All Beneficiaries"
8. **icon** (#sort_button) — label: "Sort"
9. **card** (#beneficiary_row) — label: "Beneficiary", content: "Beneficiary"
10. **text** (#no_payees_row) — label: "No beneficiaries on this account yet. Switch accounts above.", content: "No beneficiaries on this account yet. Switch accounts above."
11. **text** (#no_match_row) — label: "No beneficiaries match your search.", content: "No beneficiaries match your search."

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
- [ ] **Archetype honored:** the layout follows the "index_list" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
