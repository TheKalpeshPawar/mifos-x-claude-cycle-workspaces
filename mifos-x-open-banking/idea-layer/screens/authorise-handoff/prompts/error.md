---
ui_yaml_sha: 404ab4ba87622042984f31baeb5bda7c4bf761b8e34b5068c11d2a23330b3b20
design_md_hash: 2b17083785e7e532a1554540e628db54640dfab77857b6c90d802767add94ba2
app_shell_hash: 33fdcb113930d6c243094587e9fb8386d41a289204b1484e98129c79f97bea84
design_read_hash: 60a4c95f7619b31daccc130861a96508d0cacf2f29734f43c35036c1f0280375
content_hash: c2a7bbd04ff12bca67345185c2f37c954f6b55fb6c3fc2dce58eb20e19c075ed

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: authorise-handoff
state: error
state_visibility: error

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# authorise-handoff — error state

> Auto-generated from screens/authorise-handoff/ui.yaml @ SHA d252789987e96316
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
3. **text** (#handoff_title) — content: "Getting ready to connect securely"
4. **text** (#handoff_message) — content: "You'll sign in directly with HSBC to approve this. Your username, password and s"
5. **card** (#handoff_summary_card)
6. **text** (#handoff_amount_value) — content: "£250.00"
7. **text** (#handoff_payee_value) — content: "To Jordan Avery"
8. **text** (#handoff_securing_label) — content: "Authorising securely with HSBC Open Banking"
9. **card** (#handoff_access_note)
10. **text** (#handoff_access_title) — content: "You're approving read-only access to:"
11. **text** (#handoff_access_list) — content: "Your account details, balances, transactions and payees · for 90 days"
12. **loading_indicator** (#handoff_spinner)
13. **button** (#handoff_continue_button) — label: "Continue to your bank"
14. **text** (#handoff_security_note) — content: "Encrypted connection · You can return here anytime"
15. **card** (#handoff_error_card)
16. **icon** (#handoff_error_icon) — content: "error"
17. **text** (#handoff_error_message) — content: "We couldn't start your secure sign-in with HSBC. No money has left your account."
18. **button** (#handoff_retry_button) — label: "Try again"
19. **button** (#handoff_cancel_link) — label: "Cancel"

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
