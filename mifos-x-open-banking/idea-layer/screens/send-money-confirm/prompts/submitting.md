---
ui_yaml_sha: 022882f7252c8e96444f47cf075e92d4dd4279e7abfbcde0b9502be83b37406b
design_md_hash: 2b17083785e7e532a1554540e628db54640dfab77857b6c90d802767add94ba2
app_shell_hash: d2fe35b34f2ccfe703fcea97291ff9cb0453b148553d7b69b40f4cfa59d08766
design_read_hash: 60a4c95f7619b31daccc130861a96508d0cacf2f29734f43c35036c1f0280375
content_hash: 794ddb3b4087c149c76384d30937df8643ac1929fa33ba18ed38a668eac2aa4c

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: detail_screen

feature: send-money-confirm
state: submitting
state_visibility: submitting

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# send-money-confirm — submitting state

> Auto-generated from screens/send-money-confirm/ui.yaml @ SHA 6afc5669f52d8d5b
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: detail_screen

## Layout
- type: scrollable_column
- padding: default
- alignment: start

## Composition (top → bottom)
1. **text** (#confirm_title) — label: "Confirm Payment"
2. **text** (#review_subtitle) — label: "Please review the payment details before confirming", content: "Please review the payment details before confirming"
3. **box** (#payment_summary_card) — label: "Payment Summary"
4. **text** (#payment_amount) — label: "£500.00", content: "£500.00"
5. **divider** (#amount_divider)
6. **stack** (#to_row) — label: "To"
7. **text** (#to_label) — label: "To", content: "To"
8. **text** (#to_value) — label: "John Smith — Barclays Bank UK", content: "John Smith — Barclays Bank UK"
9. **stack** (#iban_row) — label: "IBAN"
10. **text** (#iban_label) — label: "IBAN", content: "IBAN"
11. **text** (#iban_value) — label: "GB29 NWBK 6016 1331 9268 19", content: "GB29 NWBK 6016 1331 9268 19"
12. **stack** (#from_row) — label: "From"
13. **text** (#from_label) — label: "From", content: "From"
14. **text** (#from_value) — label: "Primary Checking (...0130)", content: "Primary Checking (...0130)"
15. **stack** (#reference_row) — label: "Reference"
16. **text** (#reference_label) — label: "Reference", content: "Reference"
17. **text** (#reference_value) — label: "Rent August 2026", content: "Rent August 2026"
18. **stack** (#sent_via_row) — label: "Sent via"
19. **text** (#sent_via_label) — label: "Sent via", content: "Sent via"
20. **text** (#sent_via_value) — label: "SEPA", content: "SEPA"
21. **divider** (#fee_divider)
22. **stack** (#fee_row) — label: "Fee"
23. **text** (#fee_label) — label: "Fee", content: "Fee"
24. **text** (#fee_value) — label: "£0.00", content: "£0.00"
25. **text** (#conversion_note) — label: "Converted from GBP at today's rate", content: "Converted from GBP at today's rate"
26. **stack** (#total_row) — label: "Total"
27. **text** (#total_label) — label: "Total", content: "Total"
28. **text** (#total_value) — label: "£500.00", content: "£500.00"
29. **box** (#payment_error) — label: "Payment error", content: "Payment could not be processed. Please try again."
30. **text** (#terms_text) — label: "By confirming you authorise this payment per our Terms of Service", content: "By confirming you authorise this payment per our Terms of Service"
31. **button** (#confirm_send_button) — label: "Confirm & Send"
32. **button** (#edit_payment_button) — label: "Edit Payment"

## State-specific behavior
- Custom state "Submitting" — render per the composition below.

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

- [ ] **Per-state shape:** the render shows ONLY this state ("submitting"). Do not blend multiple states into one mockup.
- [ ] **Real content:** every text label, image, and data point reflects the content source manifest above — no numbered generic items, no filler text, no dummy text, no empty strings.
- [ ] **Token fidelity:** colors come from the uploaded design system (primary/secondary/surface/etc.) by name; spacing comes from declared scale tokens. No invented hex codes, no invented size literals.
- [ ] **Component vocabulary:** every component in the render maps to a named design-system component (Card, FAB, BottomBar, etc.) — no invented or off-system components.
- [ ] **Archetype honored:** the layout follows the "detail_screen" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
