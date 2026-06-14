---
ui_yaml_sha: 2f471367e3c2ed317053d0bdc8c5fafb2aaef1edaacbca626c6aaa5cb3e00920
design_md_hash: 2b17083785e7e532a1554540e628db54640dfab77857b6c90d802767add94ba2
app_shell_hash: d2fe35b34f2ccfe703fcea97291ff9cb0453b148553d7b69b40f4cfa59d08766
design_read_hash: 60a4c95f7619b31daccc130861a96508d0cacf2f29734f43c35036c1f0280375
content_hash: 81a076d4717d990165c2bc1b357e8de75c31e996902177e3d96522ab396608a9

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: onboarding

feature: consent-intro
state: content
state_visibility: content

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# consent-intro — content state

> Auto-generated from screens/consent-intro/ui.yaml @ SHA 824168939b11caca
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: onboarding

## Layout
- type: column
- padding: spacing.lg
- alignment: start

## Composition (top → bottom)
1. **stack** (#intro_root)
2. **icon** (#intro_hero_icon) — content: "account_balance"
3. **text** (#intro_title) — content: "Connect your HSBC account"
4. **text** (#intro_subtitle) — content: "Link your HSBC account securely through Open Banking to see your balances, trans"
5. **card** (#intro_trust_card)
6. **text** (#intro_trust_heading) — content: "You stay in control"
7. **text** (#intro_trust_point_one) — content: "You approve access at HSBC — not here. Sign-in and approval happen on HSBC's own"
8. **text** (#intro_trust_point_two) — content: "You choose exactly what to share. Pick which accounts and details to connect on "
9. **text** (#intro_trust_point_three) — content: "Read-only unless you authorise a payment. We can view your data; money only move"
10. **text** (#intro_trust_point_four) — content: "Revoke access any time in Settings — disconnecting takes effect immediately."
11. **card** (#intro_access_card)
12. **text** (#intro_access_heading) — content: "What we'll read"
13. **list** (#intro_access_list)
14. **card** (#intro_redirect_card)
15. **icon** (#intro_redirect_icon) — content: "open_in_browser"
16. **text** (#intro_redirect_text) — content: "Next, you'll be taken to HSBC's own secure sign-in to approve this connection. W"
17. **text** (#intro_security_note) — content: "You can review exactly what you're sharing on the next screen before anything is"
18. **button** (#intro_connect_button) — label: "Connect your HSBC account"
19. **stack** (#intro_legal_links)
20. **link** (#intro_terms_link) — label: "Terms of Service"
21. **link** (#intro_privacy_link) — label: "Privacy Policy"
22. **text** (#intro_footer) — content: "Powered by Open Banking"

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
- [ ] **Archetype honored:** the layout follows the "onboarding" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
