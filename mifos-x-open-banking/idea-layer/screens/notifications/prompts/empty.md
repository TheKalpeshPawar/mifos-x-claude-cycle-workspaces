---
ui_yaml_sha: b924b1a78850d7e7b49f6324bfe725251eab8dda964294105a62d7c0d693e758
design_md_hash: 2b17083785e7e532a1554540e628db54640dfab77857b6c90d802767add94ba2
app_shell_hash: d2fe35b34f2ccfe703fcea97291ff9cb0453b148553d7b69b40f4cfa59d08766
design_read_hash: 60a4c95f7619b31daccc130861a96508d0cacf2f29734f43c35036c1f0280375
content_hash: 619fe664f2027d3e3bff799478f8007ede163168dd39340bc1ff407480921976

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: notifications
state: empty
state_visibility: empty

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# notifications — empty state

> Auto-generated from screens/notifications/ui.yaml @ SHA 041f09ec74d364ed
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: index_list

## Layout
- type: scrollable_column
- padding: default
- alignment: start

## Composition (top → bottom)
1. **stack** (#title_action_row) — label: "Notifications header row"
2. **text** (#notifications_title) — label: "Notifications", content: "Notifications"
3. **button** (#mark_all_read_button) — label: "Mark All Read"
4. **text** (#section_today_label) — label: "Today", content: "Today"
5. **box** (#notification_payment_james) — label: "Payment received from James Wilson", content: "Payment received from James Wilson"
6. **stack** (#payment_james_row) — label: "Payment from James Wilson row"
7. **box** (#payment_james_icon_bg) — label: "Payment received icon background"
8. **icon** (#payment_james_icon) — label: "Incoming payment"
9. **stack** (#payment_james_text_col) — label: "Payment from James Wilson text"
10. **text** (#payment_james_title) — label: "Payment received", content: "Payment received"
11. **text** (#payment_james_message) — label: "Payment of £50.00 received from James Wilson", content: "Payment of £50.00 received from James Wilson"
12. **text** (#payment_james_time) — label: "10 min ago", content: "10 min ago"
13. **box** (#unread_dot_payment_james) — label: "Unread indicator"
14. **text** (#section_earlier_label) — label: "Earlier", content: "Earlier"
15. **box** (#notification_netflix_mandate) — label: "Direct debit mandate created for Netflix", content: "Direct debit mandate created for Netflix"
16. **stack** (#netflix_mandate_row) — label: "Netflix mandate notification row"
17. **box** (#netflix_mandate_icon_bg) — label: "Direct debit mandate icon background"
18. **icon** (#netflix_mandate_icon) — label: "Direct debit"
19. **stack** (#netflix_mandate_text_col) — label: "Netflix mandate notification text"
20. **text** (#netflix_mandate_title) — label: "Direct debit mandate created", content: "Direct debit mandate created"
21. **text** (#netflix_mandate_message) — label: "Direct debit mandate created for Netflix — £15.99/month from your Current Accoun", content: "Direct debit mandate created for Netflix — £15.99/month from your Current Accoun"
22. **text** (#netflix_mandate_time) — label: "3 hr ago", content: "3 hr ago"
23. **box** (#notification_salary_credited) — label: "Salary credited notification", content: "Salary credited notification"
24. **stack** (#salary_credited_row) — label: "Salary credited notification row"
25. **box** (#salary_credited_icon_bg) — label: "Salary credited icon background"
26. **icon** (#salary_credited_icon) — label: "Incoming payment"
27. **stack** (#salary_credited_text_col) — label: "Salary credited text"
28. **text** (#salary_credited_title) — label: "Salary credited", content: "Salary credited"
29. **text** (#salary_credited_message) — label: "£3,200.00 from Acme Ltd has been credited to your Current Account.", content: "£3,200.00 from Acme Ltd has been credited to your Current Account."
30. **text** (#salary_credited_time) — label: "Yesterday", content: "Yesterday"
31. **spacer** (#bottom_spacer)

## State-specific behavior
- Show an empty-state illustration, a friendly message, and one primary call-to-action button.

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

- [ ] **Per-state shape:** the render shows ONLY this state ("empty"). Do not blend multiple states into one mockup.
- [ ] **Real content:** every text label, image, and data point reflects the content source manifest above — no numbered generic items, no filler text, no dummy text, no empty strings.
- [ ] **Token fidelity:** colors come from the uploaded design system (primary/secondary/surface/etc.) by name; spacing comes from declared scale tokens. No invented hex codes, no invented size literals.
- [ ] **Component vocabulary:** every component in the render maps to a named design-system component (Card, FAB, BottomBar, etc.) — no invented or off-system components.
- [ ] **Archetype honored:** the layout follows the "index_list" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
