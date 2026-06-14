---
ui_yaml_sha: 650c4bde7c77090af9b13a51a7cc3fa8ad7925bd9134bca5fff33a03eb229bd0
design_md_hash: 2b17083785e7e532a1554540e628db54640dfab77857b6c90d802767add94ba2
app_shell_hash: d2fe35b34f2ccfe703fcea97291ff9cb0453b148553d7b69b40f4cfa59d08766
design_read_hash: 60a4c95f7619b31daccc130861a96508d0cacf2f29734f43c35036c1f0280375
content_hash: d0785246a50ef5f6bd41408d711f66a074a16a7699cb1641155edd68c809f7c4

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: direct-debits
state: empty
state_visibility: empty

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# direct-debits — empty state

> Auto-generated from screens/direct-debits/ui.yaml @ SHA d8f8673fe4d7236d
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

## Archetype: index_list

## Layout
- type: scrollable_column
- padding: default
- alignment: start

## Composition (top → bottom)
1. **stack** (#mandates_header_row) — label: "Your mandates header"
2. **text** (#mandates_title) — label: "Your mandates", content: "Your mandates"
3. **badge** (#active_count_chip) — label: "active count", content: "3 active"
4. **list** (#mandates_list) — label: "Direct debit mandates"
5. **card** (#mandate_card) — label: "Mandate card"
6. **text** (#mandate_merchant) — label: "Merchant name", content: "Netflix"
7. **badge** (#mandate_status_badge) — label: "Status badge", content: "Active"
8. **icon** (#mandate_cancel_icon) — label: "Cancel mandate"
9. **text** (#mandate_amount) — label: "Amount / frequency", content: "£15.99 / month"
10. **text** (#mandate_next_date) — label: "Next collection", content: "Next: 3 Jun 2026"
11. **text** (#mandate_ref) — label: "Mandate reference", content: "Ref: DD-NF-20240301"
12. **dialog** (#cancel_confirm_dialog) — title: "Cancel Direct Debit?", label: "Cancel Direct Debit?"
13. **button** (#cancel_confirm_cta) — label: "Yes, Cancel Mandate"
14. **button** (#cancel_dismiss_cta) — label: "Keep Mandate"
15. **empty_state** (#empty_state) — label: "No direct debits"
16. **error_state** (#error_state) — label: "Unable to load"

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
