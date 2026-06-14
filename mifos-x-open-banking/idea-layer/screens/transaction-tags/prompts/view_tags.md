---
ui_yaml_sha: 46ee3d0362b3802f13f4ea059e23b636ac0458550c4aa5341eaee4edcddf1f3d
design_md_hash: 2b17083785e7e532a1554540e628db54640dfab77857b6c90d802767add94ba2
app_shell_hash: d2fe35b34f2ccfe703fcea97291ff9cb0453b148553d7b69b40f4cfa59d08766
design_read_hash: 60a4c95f7619b31daccc130861a96508d0cacf2f29734f43c35036c1f0280375
content_hash: 18aa5d0d1b6eea3174428026fafac888cf381fffdf690179139070eef20611eb

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: detail_screen

feature: transaction-tags
state: view_tags
state_visibility: view_tags

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# transaction-tags — view_tags state

> Auto-generated from screens/transaction-tags/ui.yaml @ SHA f3a5e616c9a79f6f
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: detail_screen

## Layout
- type: scrollable_column
- padding: default
- alignment: start

## Composition (top → bottom)
1. **box** (#transaction_header_card) — label: "Transaction header", content: "Transaction header"
2. **text** (#txn_merchant) — label: "Whole Foods Market", content: "Whole Foods Market"
3. **text** (#txn_amount) — label: "-£67.84", content: "-£67.84"
4. **text** (#txn_date) — label: "23 May 2026 · 14:32", content: "23 May 2026 · 14:32"
5. **text** (#tags_section_label) — label: "Tags", content: "Tags"
6. **text** (#tags_hint_text) — label: "Tap a tag to remove it", content: "Tap a tag to remove it"
7. **stack** (#tags_chips_row) — label: "Existing tags"
8. **box** (#tag_chip_groceries) — label: "#groceries", content: "#groceries"
9. **box** (#tag_chip_work_expense) — label: "#work-expense", content: "#work-expense"
10. **box** (#tag_chip_rent) — label: "#rent", content: "#rent"
11. **box** (#tag_chip_holiday) — label: "#holiday", content: "#holiday"
12. **box** (#tag_chip_gym) — label: "#gym", content: "#gym"
13. **stack** (#add_tag_row) — label: "Add tag row"
14. **input** (#add_tag_input) — label: "Add tag"
15. **button** (#add_tag_button) — label: "Add"
16. **divider** (#notes_divider)
17. **text** (#notes_section_label) — label: "Notes", content: "Notes"
18. **input** (#notes_text_area) — label: "Transaction notes"
19. **divider** (#receipt_divider)
20. **text** (#receipt_section_label) — label: "Receipt", content: "Receipt"
21. **box** (#receipt_attachment_area) — label: "Receipt attachment area", content: "Receipt attachment area"
22. **icon** (#receipt_placeholder_icon) — label: "Receipt icon"
23. **text** (#receipt_placeholder_text) — label: "No receipt attached", content: "Tap to attach a receipt image"
24. **button** (#camera_button) — label: "Take Photo"
25. **button** (#save_button) — label: "Save"
26. **box** (#save_success_banner) — label: "Tags and notes saved", content: "Tags and notes saved"
27. **icon** (#save_success_icon) — label: "Success"

## State-specific behavior
- Custom state "View Tags" — render per the composition below.

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

- [ ] **Per-state shape:** the render shows ONLY this state ("view_tags"). Do not blend multiple states into one mockup.
- [ ] **Real content:** every text label, image, and data point reflects the content source manifest above — no numbered generic items, no filler text, no dummy text, no empty strings.
- [ ] **Token fidelity:** colors come from the uploaded design system (primary/secondary/surface/etc.) by name; spacing comes from declared scale tokens. No invented hex codes, no invented size literals.
- [ ] **Component vocabulary:** every component in the render maps to a named design-system component (Card, FAB, BottomBar, etc.) — no invented or off-system components.
- [ ] **Archetype honored:** the layout follows the "detail_screen" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
