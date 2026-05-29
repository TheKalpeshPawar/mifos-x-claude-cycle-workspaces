---
ui_yaml_sha: 610d54f97461af152d8413cddf97ce826c1911adb639f69fe46a26dba9a5cfcb
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: ad5b41232573337c86c391de430c5ac2410dbd2fb4c6a5be242fe4c17fc67aa8

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: meetings
state: content
state_visibility: content

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# meetings — content state

> Auto-generated from screens/meetings/ui.yaml @ SHA 021bc575446cd2de
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the meetings screen for **Mifos X Open Banking**, a Open Banking KMP super-app for consumer retail banking and field officer agent banking in emerging markets.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, error #FFB4AB, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, outline #8F9285, pending #E8A317.

**Component 1 — App Bar** (full width, 56dp tall): Title "Meetings - May 2026" Outfit Medium 18sp #E3E3D8 left-aligned 16dp padding. Background #12140E. Zero elevation.

**Component 2 — Chip Row** (full width minus 32dp insets, top margin 16dp, 12dp gap, horizontally scrollable): 7 day chips each 44dp x 56dp, 12dp corner radius. "Sun 25" selected filled #354E16, label "Sun" Outfit Regular 11sp #CDEDA3 date "25" Outfit SemiBold 16sp #B2D188. Other days Mon 19, Tue 20, Wed 21, Thu 22, Fri 23, Sat 24 each outlined 1dp #44483D background #1E201A label Outfit Regular 11sp #C5C8BA date Outfit Medium 16sp #E3E3D8. Button "Today" Outfit Medium 12sp #B2D188 right-aligned 16dp padding.

**Component 3 — Section Header** (full width minus 32dp insets, top margin 20dp): Section header "3 meetings this week" Outfit SemiBold 14sp #E3E3D8.

**Component 4 — Card** (full width minus 32dp insets, top margin 12dp, 12dp corner radius, background #1E201A, 16dp padding): Meeting card 1. Row: time "10:00 AM" Outfit SemiBold 14sp #B2D188 left, chip "Online" Outfit Regular 11sp #A0CFCB filled #1F4E4B right. Title "Account Opening Meeting" Outfit SemiBold 16sp #E3E3D8 top margin 8dp. Customer "John Mwangi · 1 hr · Google Meet" Outfit Regular 13sp #C5C8BA top margin 4dp. Action row top margin 12dp: Button "Join" Outfit SemiBold 14sp #1F3701 filled #B2D188 36dp tall 12dp corner radius, Button "Notes" Outfit SemiBold 14sp #CDEDA3 outlined #354E16 36dp tall 12dp corner radius.

**Component 5 — Card** (full width minus 32dp insets, top margin 12dp, same style): Meeting card 2. Row: time "2:00 PM" #B2D188 left, chip "In-Person" #A0CFCB filled #1F4E4B right. Title "KYC Review" Outfit SemiBold 16sp #E3E3D8. Customer "Sarah Odhiambo · 30 min · Nairobi Branch, Kimathi St" Outfit Regular 13sp #C5C8BA.

**Component 6 — Card** (full width minus 32dp insets, top margin 12dp, same style): Meeting card 3. Row: time "Tomorrow · 11:00 AM" #B2D188 left, chip "Phone" #A0CFCB filled #1F4E4B right. Title "New Prospect - Introductory Call" Outfit SemiBold 16sp #E3E3D8. Customer "Peter Kamau · Referral from Equity Bank" Outfit Regular 13sp #C5C8BA.

**Component 7 — FAB** (bottom-right, 56dp diameter, 24dp corner radius, background #B2D188): FAB with calendar_add icon 24dp #1F3701 and label "Schedule Meeting" Outfit SemiBold 14sp #1F3701 extended FAB 56dp tall 999dp radius.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Full scrollable layout on #12140E. The earth-green #B2D188 on time stamps, selected day, and FAB creates a focused operational rhythm, keeping the interface calm and balanced for field officers navigating their daily schedule.

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
- [ ] **Archetype honored:** the layout follows the "screen" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

Anchored by the accent #B2D188 on time stamps and the selected day chip, the layout stays calm and balanced throughout the meetings view.

↑↑↑ MOCKUP PROMPT
