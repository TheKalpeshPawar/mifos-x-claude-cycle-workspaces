---
ui_yaml_sha: 8e7e5035f3814713301638fb1d901141132dd3a223b1fd7a604d21f138169ff2
design_md_hash: 2b17083785e7e532a1554540e628db54640dfab77857b6c90d802767add94ba2
app_shell_hash: d2fe35b34f2ccfe703fcea97291ff9cb0453b148553d7b69b40f4cfa59d08766
design_read_hash: 60a4c95f7619b31daccc130861a96508d0cacf2f29734f43c35036c1f0280375
content_hash: e35e6cf54f91ce1ef9e67a18c49823c7213ecf46a16b6c2765358b3b702916b4

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: index_list

feature: atm-locator
state: unauthenticated
state_visibility: unauthenticated

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# atm-locator — unauthenticated state

> Auto-generated from screens/atm-locator/ui.yaml @ SHA 7b24b41d48301215
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: index_list

## Layout
- type: scrollable_column
- padding: default
- alignment: start

## Composition (top → bottom)
1. **text** (#atm_locator_title) — content: "ATM & Branches"
2. **image** (#atm_map_area) — content: "ATM map"
3. **stack** (#atm_search_row)
4. **input** (#location_search_input) — label: "Search location"
5. **icon_button** (#use_my_location_button) — content: "my_location"
6. **text** (#nearby_results_header) — content: "4 ATMs near you"
7. **box** (#atm_result_kcb_westlands)
8. **text** (#atm_kcb_name) — content: "KCB Westlands ATM"
9. **text** (#atm_kcb_hours) — content: "Open 24 hours"
10. **badge** (#atm_kcb_distance) — content: "320 m"
11. **text** (#atm_kcb_address) — content: "Westlands Commercial Centre, Waiyaki Way, Nairobi, Nairobi County, 00100"
12. **chip** (#atm_kcb_accessible_chip) — label: "Accessible", content: "accessible"
13. **chip** (#atm_kcb_deposits_chip) — label: "Deposits", content: "deposits"
14. **button** (#atm_kcb_directions) — label: "Directions"
15. **box** (#atm_result_equity_cbd)
16. **text** (#atm_equity_name) — content: "Equity Bank CBD ATM"
17. **text** (#atm_equity_hours) — content: "Open 24 hours"
18. **badge** (#atm_equity_distance) — content: "1.2 km"
19. **box** (#atm_result_coop_karen)
20. **text** (#atm_coop_name) — content: "Co-op Bank Karen ATM"
21. **text** (#atm_coop_hours) — content: "Daily 06:00–22:00"
22. **badge** (#atm_coop_distance) — content: "6.4 km"
23. **stack** (#atm_empty_state)
24. **icon** (#atm_empty_icon) — content: "location_off"
25. **text** (#atm_empty_title) — content: "No ATMs nearby"
26. **text** (#atm_empty_message) — content: "None of your banks have published ATM locations yet."
27. **stack** (#atm_error_state)
28. **icon** (#atm_error_icon) — content: "cloud_off"
29. **text** (#atm_error_title) — content: "Couldn't load ATMs"
30. **text** (#atm_error_message) — content: "Check your connection and try again"
31. **button** (#atm_retry_button) — label: "Retry"

## State-specific behavior
- Custom state "Unauthenticated" — render per the composition below.

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

- [ ] **Per-state shape:** the render shows ONLY this state ("unauthenticated"). Do not blend multiple states into one mockup.
- [ ] **Real content:** every text label, image, and data point reflects the content source manifest above — no numbered generic items, no filler text, no dummy text, no empty strings.
- [ ] **Token fidelity:** colors come from the uploaded design system (primary/secondary/surface/etc.) by name; spacing comes from declared scale tokens. No invented hex codes, no invented size literals.
- [ ] **Component vocabulary:** every component in the render maps to a named design-system component (Card, FAB, BottomBar, etc.) — no invented or off-system components.
- [ ] **Archetype honored:** the layout follows the "index_list" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
