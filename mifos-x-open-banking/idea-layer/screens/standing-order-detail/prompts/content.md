---
ui_yaml_sha: c09fb6b7e523aa0f743a826db9c04ae127623f0116429593eabff09a11292fc7
design_md_hash: 2b17083785e7e532a1554540e628db54640dfab77857b6c90d802767add94ba2
app_shell_hash: d2fe35b34f2ccfe703fcea97291ff9cb0453b148553d7b69b40f4cfa59d08766
design_read_hash: 60a4c95f7619b31daccc130861a96508d0cacf2f29734f43c35036c1f0280375
content_hash: c7c7ac6ce70b1b2a6dcb0c4215a384a5cc83217e76ac8a764f05543a44e18af7

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: detail_screen

feature: standing-order-detail
state: content
state_visibility: content

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# standing-order-detail — content state

> Auto-generated from screens/standing-order-detail/ui.yaml @ SHA 6c24735ff64d0039
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: detail_screen

## Layout
- type: column
- padding: default
- alignment: start

## Composition (top → bottom)
1. **stack** (#sod_root)
2. **card** (#sod_recipient_card)
3. **text** (#sod_recipient_header) — content: "RECIPIENT"
4. **stack** (#sod_recipient_name_row)
5. **text** (#sod_recipient_name_label) — content: "Name"
6. **text** (#sod_recipient_name_value) — content: "Landlord Holdings Ltd"
7. **stack** (#sod_recipient_account_row)
8. **text** (#sod_recipient_account_label) — content: "Account"
9. **text** (#sod_recipient_account_value) — content: "····s001"
10. **card** (#sod_schedule_card)
11. **text** (#sod_schedule_header) — content: "SCHEDULE"
12. **stack** (#sod_status_row)
13. **text** (#sod_status_label) — content: "Status"
14. **text** (#sod_status_value) — content: "Active"
15. **stack** (#sod_frequency_row)
16. **text** (#sod_frequency_label) — content: "Frequency"
17. **text** (#sod_frequency_value) — content: "Monthly"
18. **stack** (#sod_first_payment_row)
19. **text** (#sod_first_payment_label) — content: "First Payment"
20. **text** (#sod_first_payment_value) — content: "1 Jan 2026"
21. **stack** (#sod_last_payment_row)
22. **text** (#sod_last_payment_label) — content: "Last Payment"
23. **text** (#sod_last_payment_value) — content: "1 May 2026"
24. **stack** (#sod_next_payment_row)
25. **text** (#sod_next_payment_label) — content: "Next Payment"
26. **text** (#sod_next_payment_value) — content: "1 Jun 2026"
27. **stack** (#sod_final_date_row)
28. **text** (#sod_final_date_label) — content: "Final Date"
29. **text** (#sod_final_date_value) — content: "Ongoing"
30. **card** (#sod_amount_card)
31. **text** (#sod_amount_header) — content: "PAYMENT AMOUNT"
32. **stack** (#sod_amount_value_row)
33. **text** (#sod_amount_value) — content: "£1,200.00"
34. **badge** (#sod_currency_badge) — content: "GBP"
35. **card** (#sod_history_card)
36. **text** (#sod_history_header) — content: "RECENT EXECUTIONS"
37. **list** (#sod_history_list)
38. **list_item** (#sod_history_row)
39. **text** (#sod_history_row_date) — content: "1 May 2026"
40. **text** (#sod_history_row_status) — content: "Completed"
41. **text** (#sod_history_row_amount) — content: "£1,200.00"
42. **stack** (#sod_action_row)
43. **button** (#sod_pause_resume_button) — label: "Pause"
44. **button** (#sod_cancel_button) — label: "Cancel"
45. **spacer** (#sod_bottom_spacer)
46. **skeleton** (#sod_loading_skeleton)
47. **stack** (#sod_error_state)
48. **icon** (#sod_error_icon) — content: "cloud_off"
49. **text** (#sod_error_title) — content: "Standing Order Not Found"
50. **text** (#sod_error_message) — content: "We could not load this standing order. It may have been cancelled or there may b"
51. **button** (#sod_retry_button) — label: "Retry"
52. **stack** (#sod_empty_state)
53. **icon** (#sod_empty_icon) — content: "cloud_off"
54. **text** (#sod_empty_message) — content: "No details are available for this standing order."
55. **button** (#sod_back_to_list_button) — label: "Go Back"

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
- [ ] **Archetype honored:** the layout follows the "detail_screen" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
