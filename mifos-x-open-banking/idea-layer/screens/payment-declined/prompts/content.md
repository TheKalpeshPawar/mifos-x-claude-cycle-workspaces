---
ui_yaml_sha: 82672fbfacaaf9c23b68abad2ae0208c7007b5cde4dd7d5d67ed30480a8b1b38
design_md_hash: 2b17083785e7e532a1554540e628db54640dfab77857b6c90d802767add94ba2
app_shell_hash: d2fe35b34f2ccfe703fcea97291ff9cb0453b148553d7b69b40f4cfa59d08766
design_read_hash: 60a4c95f7619b31daccc130861a96508d0cacf2f29734f43c35036c1f0280375
content_hash: 69e615324bfc41034d104f7c6e77751c52e390f23cc3976f0d0c6f9bd137a7f9

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: error

feature: payment-declined
state: content
state_visibility: content

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# payment-declined — content state

> Auto-generated from screens/payment-declined/ui.yaml @ SHA 20c2427fb97c95d1
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: error

## Layout
- type: column
- padding: spacing.lg
- alignment: start

## Composition (top → bottom)
1. **stack** (#declined_root)
2. **icon** (#declined_icon) — content: "cancel"
3. **text** (#declined_title) — content: "Payment not completed"
4. **text** (#declined_assurance) — content: "Good news: no money has left your account."
5. **text** (#declined_message) — content: "You didn't finish authorising this payment at HSBC, so it wasn't sent. You can r"
6. **card** (#declined_details_card)
7. **text** (#declined_amount_value) — content: "£250.00"
8. **text** (#declined_payee_value) — content: "To Jordan Avery — Barclays Bank UK"
9. **stack** (#declined_reason_row)
10. **text** (#declined_reason_label) — content: "Reason"
11. **text** (#declined_reason_value) — content: "Authorisation cancelled at HSBC"
12. **card** (#declined_reasons_card)
13. **text** (#declined_reasons_heading) — content: "This can happen if:"
14. **text** (#declined_reason_one) — content: "You chose to cancel on the HSBC approval screen"
15. **text** (#declined_reason_two) — content: "The approval timed out before it was confirmed"
16. **text** (#declined_reason_three) — content: "HSBC couldn't confirm the payment from your account"
17. **text** (#declined_status_note) — content: "Reference: access_denied (consent RJCT)"
18. **button** (#declined_try_again_button) — label: "Try again"
19. **button** (#declined_done_button) — label: "Back to home"

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
- [ ] **Archetype honored:** the layout follows the "error" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
