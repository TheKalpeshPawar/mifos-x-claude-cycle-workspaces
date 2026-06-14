---
ui_yaml_sha: d421a4c0c9ef8d437612d10ec91aabbefc81f46db71529fdf7081c8d737ba922
design_md_hash: 2b17083785e7e532a1554540e628db54640dfab77857b6c90d802767add94ba2
app_shell_hash: d2fe35b34f2ccfe703fcea97291ff9cb0453b148553d7b69b40f4cfa59d08766
design_read_hash: 60a4c95f7619b31daccc130861a96508d0cacf2f29734f43c35036c1f0280375
content_hash: bac12e3d0dc8e711667d703c95eb5482180775aa34aba796a74002a39f545e4e

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: direct-debit-detail
state: loading
state_visibility: loading

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# direct-debit-detail — loading state

> Auto-generated from screens/direct-debit-detail/ui.yaml @ SHA f3f84c7c376d7a11
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: detail_screen

## Layout
- type: column
- padding: spacing.lg
- alignment: start

## Composition (top → bottom)
1. **stack** (#ddd_root)
2. **stack** (#ddd_merchant_hero)
3. **text** (#ddd_merchant_name) — content: "Netflix"
4. **badge** (#ddd_mandate_status_badge) — content: "Active"
5. **text** (#ddd_mandate_amount_value) — content: "£15.99"
6. **text** (#ddd_mandate_frequency_text) — content: "Monthly"
7. **card** (#ddd_mandate_details_card)
8. **text** (#ddd_details_header) — content: "Mandate Details"
9. **stack** (#ddd_next_payment_row)
10. **text** (#ddd_next_payment_label) — content: "Next Payment"
11. **text** (#ddd_next_payment_value) — content: "15 Jun 2026"
12. **divider** (#ddd_divider_1)
13. **stack** (#ddd_account_row)
14. **text** (#ddd_account_label) — content: "Account"
15. **stack** (#ddd_account_value_group)
16. **text** (#ddd_account_name) — content: "Current Account"
17. **text** (#ddd_account_number) — content: "••••4521"
18. **divider** (#ddd_divider_2)
19. **stack** (#ddd_mandate_ref_row)
20. **text** (#ddd_mandate_ref_label) — content: "Mandate Ref"
21. **text** (#ddd_mandate_ref_value) — content: "DD-NF-20240301"
22. **divider** (#ddd_divider_3)
23. **stack** (#ddd_start_date_row)
24. **text** (#ddd_start_date_label) — content: "Start Date"
25. **text** (#ddd_start_date_value) — content: "1 Mar 2024"
26. **card** (#ddd_payment_history_card)
27. **stack** (#ddd_history_header_row)
28. **text** (#ddd_history_header) — content: "Recent Payments"
29. **link** (#ddd_history_view_all_link) — label: "View all"
30. **list** (#ddd_history_list)
31. **list_item** (#ddd_history_row)
32. **text** (#ddd_history_row_date) — content: "15 May 2026"
33. **text** (#ddd_history_row_amount) — content: "-£15.99"
34. **button** (#ddd_cancel_button) — label: "Cancel Mandate"
35. **dialog** (#ddd_cancel_dialog) — title: "Cancel Direct Debit?", label: "Cancel Direct Debit?"
36. **button** (#ddd_cancel_confirm_cta) — label: "Yes, Cancel Mandate"
37. **button** (#ddd_cancel_dismiss_cta) — label: "Keep Mandate"
38. **skeleton** (#ddd_loading_skeleton)
39. **stack** (#ddd_error_state)
40. **icon** (#ddd_error_icon) — content: "cloud_off"
41. **text** (#ddd_error_title) — content: "Unable to load mandate"
42. **text** (#ddd_error_message) — content: "Check your connection and try again"
43. **button** (#ddd_retry_button) — label: "Retry"
44. **stack** (#ddd_empty_state)
45. **icon** (#ddd_empty_icon) — content: "event_busy"
46. **text** (#ddd_empty_title) — content: "Mandate not available"
47. **text** (#ddd_empty_message) — content: "This direct debit could not be found. It may have already been cancelled or expi"
48. **button** (#ddd_empty_back_button) — label: "Back to Direct Debits"

## State-specific behavior
- Show shimmer/skeleton loaders matching the content layout block-for-block — no real text, no images. This is the screen's initial state.

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

- [ ] **Per-state shape:** the render shows ONLY this state ("loading"). Do not blend multiple states into one mockup.
- [ ] **Real content:** every text label, image, and data point reflects the content source manifest above — no numbered generic items, no filler text, no dummy text, no empty strings.
- [ ] **Token fidelity:** colors come from the uploaded design system (primary/secondary/surface/etc.) by name; spacing comes from declared scale tokens. No invented hex codes, no invented size literals.
- [ ] **Component vocabulary:** every component in the render maps to a named design-system component (Card, FAB, BottomBar, etc.) — no invented or off-system components.
- [ ] **Archetype honored:** the layout follows the "detail_screen" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
