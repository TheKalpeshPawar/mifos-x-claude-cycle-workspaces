---
ui_yaml_sha: b402b63bdbb81f1f06057089992eebe6129d22e389ec919550608716158c24dd
design_md_hash: 2b17083785e7e532a1554540e628db54640dfab77857b6c90d802767add94ba2
app_shell_hash: 33fdcb113930d6c243094587e9fb8386d41a289204b1484e98129c79f97bea84
design_read_hash: 60a4c95f7619b31daccc130861a96508d0cacf2f29734f43c35036c1f0280375
content_hash: 0d7906315853ac87fa2d759c26c5cef7b0665a6ea2aba153e193042d9fd2db34

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: form

feature: pay-international
state: content
state_visibility: content

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# pay-international — content state

> Auto-generated from screens/pay-international/ui.yaml @ SHA 418658b5cf94c577
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: form

## Layout
- type: scrollable_column
- padding: default
- alignment: start

## Composition (top → bottom)
1. **list_item** (#from_account_selector) — label: "From account", content: "Everyday Current — £2,483.57"
2. **input** (#amount_input) — label: "You send"
3. **text** (#recipient_label) — label: "Recipient gets", content: "RECIPIENT GETS"
4. **text** (#recipient_amount) — label: "Converted amount", content: "€2,902.50"
5. **box** (#fx_rate_card) — label: "Exchange rate", content: "Exchange rate: 1 GBP = 1.1700 EUR"
6. **text** (#fx_quote_note) — label: "Quote type", content: "Indicative rate · locked when you authorise at HSBC"
7. **box** (#fx_fee_banner) — label: "Estimated fee", content: "Estimated fee: £4.50 · No HSBC markup on the rate"
8. **text** (#to_label) — label: "To", content: "TO"
9. **list_item** (#beneficiary_row) — label: "International beneficiary", content: "Sofia Marchetti"
10. **text** (#beneficiary_subtitle) — label: "IBAN and BIC", content: "IT60 X054 ·· 8200 · BIC UNCRITMM · Italy"
11. **input** (#purpose_input) — label: "Purpose of payment"
12. **text** (#schedule_section_label) — label: "When to pay", content: "WHEN TO PAY"
13. **input** (#schedule_date_field) — label: "Payment date"
14. **chip_group** (#recurring_frequency_chips) — label: "Frequency", content: "Monthly · Quarterly · Yearly"
15. **button** (#review_button) — label: "Review"

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
- [ ] **Archetype honored:** the layout follows the "form" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
