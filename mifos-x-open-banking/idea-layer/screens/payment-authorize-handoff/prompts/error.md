---
ui_yaml_sha: 20a9628ebb04fe794988fb9061c05e5d7619c2933c48075fd51b977d755a04c6
design_md_hash: 2b17083785e7e532a1554540e628db54640dfab77857b6c90d802767add94ba2
app_shell_hash: d2fe35b34f2ccfe703fcea97291ff9cb0453b148553d7b69b40f4cfa59d08766
design_read_hash: 60a4c95f7619b31daccc130861a96508d0cacf2f29734f43c35036c1f0280375
content_hash: c1bfd0c980c70e131f6c88f8bf9a5e669e9bf115e7754998cec5796ac54a073f

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: payment-authorize-handoff
state: error
state_visibility: error

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# payment-authorize-handoff — error state

> Auto-generated from screens/payment-authorize-handoff/ui.yaml @ SHA f1237d6c820008e7
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: loading

## Layout
- type: column
- padding: spacing.lg
- alignment: start

## Composition (top → bottom)
1. **stack** (#handoff_root)
2. **icon** (#handoff_bank_icon) — content: "account_balance"
3. **text** (#handoff_title) — content: "Getting your payment ready to authorise"
4. **text** (#handoff_message) — content: "You'll authorise this payment directly with HSBC. Your username, password and se"
5. **card** (#handoff_summary_card)
6. **text** (#handoff_amount_value) — content: "£250.00"
7. **text** (#handoff_payee_value) — content: "To Jordan Avery"
8. **text** (#handoff_securing_label) — content: "Authorising securely with HSBC Open Banking"
9. **loading_indicator** (#handoff_spinner)
10. **button** (#handoff_continue_button) — label: "Continue to HSBC"
11. **text** (#handoff_security_note) — content: "Encrypted connection · You can return here anytime"
12. **card** (#handoff_error_card)
13. **icon** (#handoff_error_icon) — content: "error"
14. **text** (#handoff_error_message) — content: "We couldn't reach HSBC to authorise your payment. No money has left your account"
15. **button** (#handoff_retry_button) — label: "Try again"
16. **button** (#handoff_cancel_link) — label: "Cancel"

## State-specific behavior
- Show an error illustration, a short message, and a single Retry action. No content rails visible.

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

- [ ] **Per-state shape:** the render shows ONLY this state ("error"). Do not blend multiple states into one mockup.
- [ ] **Real content:** every text label, image, and data point reflects the content source manifest above — no numbered generic items, no filler text, no dummy text, no empty strings.
- [ ] **Token fidelity:** colors come from the uploaded design system (primary/secondary/surface/etc.) by name; spacing comes from declared scale tokens. No invented hex codes, no invented size literals.
- [ ] **Component vocabulary:** every component in the render maps to a named design-system component (Card, FAB, BottomBar, etc.) — no invented or off-system components.
- [ ] **Archetype honored:** the layout follows the "loading" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
