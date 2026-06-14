---
ui_yaml_sha: 298124b1346aaffc85e8daf9a1c8e571bf3b450b37fa5e3b6f2102c7df927a3e
design_md_hash: 2b17083785e7e532a1554540e628db54640dfab77857b6c90d802767add94ba2
app_shell_hash: d2fe35b34f2ccfe703fcea97291ff9cb0453b148553d7b69b40f4cfa59d08766
design_read_hash: 60a4c95f7619b31daccc130861a96508d0cacf2f29734f43c35036c1f0280375
content_hash: f9139f714c4784fc626e438f8dba77ddd2fd0d944d47c5f5397d040dbdbb67a6

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: consent-expired
state: error
state_visibility: error

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# consent-expired — error state

> Auto-generated from screens/consent-expired/ui.yaml @ SHA eab6bc7c2d555757
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: error

## Layout
- type: column
- padding: spacing.lg
- alignment: start

## Composition (top → bottom)
1. **stack** (#expired_root)
2. **icon** (#expired_hero_icon) — content: "schedule"
3. **text** (#expired_title) — content: "Time to reconnect"
4. **text** (#expired_subtitle) — content: "Your permission to access your HSBC account data has expired. Banks ask you to r"
5. **card** (#expired_info_card)
6. **text** (#expired_info_heading) — content: "When you reconnect:"
7. **text** (#expired_info_point_one) — content: "You'll approve access again at HSBC — your saved preferences stay put"
8. **text** (#expired_info_point_two) — content: "Your accounts and transaction history reload automatically once it's done"
9. **text** (#expired_status_note) — content: "Reference: consent expired (EXPD) · 12 Mar 2026"
10. **card** (#expired_check_banner)
11. **loading_indicator** (#expired_check_spinner)
12. **text** (#expired_check_message) — content: "Checking your connection status…"
13. **button** (#expired_reconnect_button) — label: "Reconnect"
14. **button** (#expired_dismiss_button) — label: "Not now"

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
- [ ] **Archetype honored:** the layout follows the "error" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

↑↑↑ MOCKUP PROMPT
