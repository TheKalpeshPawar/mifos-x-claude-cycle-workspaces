---
ui_yaml_sha: f316c63cf4b428a045711a6ca035c8032a7d7e10a53174b70f5945acf9b40fae
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: eb7039da31984f8e20f220554c611857a42706e33dd125030b976d539b8dec66

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: licenses
state: error
state_visibility: error

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# licenses — error state

> Auto-generated from screens/licenses/ui.yaml @ SHA c3cde9d0ddc81d58
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the error state of the licenses screen for **Mifos X Open Banking**, a Open Banking KMP super-app for consumer retail banking and field officer agent banking in emerging markets.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, error #FFB4AB, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, outline #8F9285, pending #E8A317.

**Component 1 — App Bar** (full width, 56dp tall): Title "Open Source Licenses" Outfit Medium 18sp #E3E3D8 centered. Leading back-arrow 24dp #B2D188. Background #12140E.

**Component 2 — Hero** (centered, top margin 64dp): 160dp x 160dp illustration of a broken code tag or disconnected plug rendered in #44483D and #8F9285 on #12140E. error_state archetype.

**Component 3 — App Bar** (centered, top margin 24dp, horizontal padding 32dp): Title "Unable to load license information" Outfit SemiBold 22sp #E3E3D8 centered, max 2 lines.

**Component 4 — List Row** (centered, top margin 8dp, horizontal padding 48dp): Subtext "Please restart the app. If the issue continues, check for an update." Outfit Regular 14sp #C5C8BA centered line-height 20sp, max 25 words.

**Component 5 — Button** (centered, top margin 32dp): Text button "Go back" Outfit Medium 14sp #8F9285, no background, no icon.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Centered layout on #12140E with generous vertical breathing room. The neutral #8F9285 go-back action keeps this non-critical error state understated, preserving the calm open banking aesthetic without alarm.

## Archetype

## Layout
- type: column
- padding: spacing.xl
- alignment: center

## Composition (top → bottom)
1. **stack** (#licenses_root)
2. **text** (#licenses_subtitle_text) — content: "Mifos X Open Banking is built on these outstanding open-source libraries."
3. **stack** (#licenses_list)
4. **list_item** (#license_item_compose)
5. **text** (#license_compose_name) — content: "Compose Multiplatform"
6. **text** (#license_compose_meta) — content: "v1.8.2 · JetBrains"
7. **badge** (#license_compose_badge) — content: "Apache 2.0"
8. **divider** (#license_divider_1)
9. **list_item** (#license_item_ktor)
10. **text** (#license_ktor_name) — content: "Ktor"
11. **text** (#license_ktor_meta) — content: "v3.2.0 · JetBrains"
12. **badge** (#license_ktor_badge) — content: "Apache 2.0"
13. **divider** (#license_divider_2)
14. **list_item** (#license_item_koin)
15. **text** (#license_koin_name) — content: "Koin"
16. **text** (#license_koin_meta) — content: "v4.1.0 · insert-koin.io"
17. **badge** (#license_koin_badge) — content: "Apache 2.0"
18. **divider** (#license_divider_3)
19. **list_item** (#license_item_store5)
20. **text** (#license_store5_name) — content: "Store5"
21. **text** (#license_store5_meta) — content: "v5.1.0 · Mobile Kotlin"
22. **badge** (#license_store5_badge) — content: "Apache 2.0"
23. **divider** (#license_divider_4)
24. **list_item** (#license_item_room)
25. **text** (#license_room_name) — content: "Room KMP"
26. **text** (#license_room_meta) — content: "v2.7.0 · Google / AndroidX"
27. **badge** (#license_room_badge) — content: "Apache 2.0"
28. **divider** (#license_divider_5)
29. **list_item** (#license_item_serialization)
30. **text** (#license_serialization_name) — content: "kotlinx.serialization"
31. **text** (#license_serialization_meta) — content: "v1.8.1 · JetBrains"
32. **badge** (#license_serialization_badge) — content: "Apache 2.0"
33. **divider** (#license_divider_6)
34. **list_item** (#license_item_coroutines)
35. **text** (#license_coroutines_name) — content: "kotlinx.coroutines"
36. **text** (#license_coroutines_meta) — content: "v1.10.1 · JetBrains"
37. **badge** (#license_coroutines_badge) — content: "Apache 2.0"
38. **divider** (#license_divider_7)
39. **list_item** (#license_item_material3)
40. **text** (#license_material3_name) — content: "Material3"
41. **text** (#license_material3_meta) — content: "v1.3.2 · Google / Compose"
42. **badge** (#license_material3_badge) — content: "Apache 2.0"
43. **skeleton** (#licenses_loading_skeleton)
44. **stack** (#licenses_error_state)
45. **icon** (#licenses_error_icon) — content: "code_off"
46. **text** (#licenses_error_message) — content: "Unable to load license information. Please restart the app."

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
- [ ] **Archetype honored:** the layout follows the "error_state" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

Anchored by the back-arrow accent #B2D188, the error state stays restrained and calm without alarming the user over non-critical license data.

↑↑↑ MOCKUP PROMPT
