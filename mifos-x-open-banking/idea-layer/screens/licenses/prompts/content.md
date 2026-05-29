---
ui_yaml_sha: f316c63cf4b428a045711a6ca035c8032a7d7e10a53174b70f5945acf9b40fae
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: d7400ecf6817fd9e9064f8a2a87c5027330d1a23d4648a4357d94f729a302290

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: index_list

feature: licenses
state: content
state_visibility: content

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# licenses — content state

> Auto-generated from screens/licenses/ui.yaml @ SHA 15f52fd30fcdc469
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the licenses screen for **Mifos X Open Banking**, a Open Banking KMP super-app for consumer retail banking and field officer agent banking in emerging markets.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, error #FFB4AB, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, outline #8F9285, pending #E8A317.

**Component 1 — App Bar** (full width, 56dp tall): Title "Open Source Licenses" Outfit Medium 18sp #E3E3D8 centered. Leading back-arrow 24dp #B2D188. Background #12140E. Subtitle "Mifos X Open Banking is built on these outstanding open-source libraries." Outfit Regular 12sp #C5C8BA below centered.

**Component 2 — List Row** (full width minus 32dp insets, top margin 16dp): 8 list item rows each 64dp tall separated by 1dp divider #44483D. index_list archetype. Each row: library name Outfit SemiBold 14sp #E3E3D8 left, meta below Outfit Regular 12sp #C5C8BA, badge right. Libraries in order: "Compose Multiplatform" meta "v1.8.2 · JetBrains" badge "Apache 2.0" Outfit Medium 11sp #CDEDA3 filled #354E16 pill 6dp padding. "Ktor" meta "v3.2.0 · JetBrains" badge "Apache 2.0" same style. "Koin" meta "v4.1.0 · insert-koin.io" badge "Apache 2.0". "Store5" meta "v5.1.0 · Mobile Kotlin" badge "Apache 2.0". "Room KMP" meta "v2.7.0 · Google / AndroidX" badge "Apache 2.0". "kotlinx.serialization" meta "v1.8.1 · JetBrains" badge "Apache 2.0". "kotlinx.coroutines" meta "v1.10.1 · JetBrains" badge "Apache 2.0". "Material3" meta "v1.3.2 · Google / Compose" badge "Apache 2.0".

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Full scrollable layout on #12140E. The soft earth-green #B2D188 on badge fills and the back-arrow acknowledges the open-source foundation with quiet gratitude calibrated to the trust-first financial aesthetic.

## State-specific behavior
- Fully populated with the real demo content listed below.

## Content source manifest
- demo-data.demo_entries[0..7]
- demo-data.demo_entries[0..7]
- demo-data.demo_entries[0..7]
- demo-data.demo_entries[0..7]
- demo-data.demo_entries[0..7]
- demo-data.demo_entries[0..7]
- demo-data.demo_entries[0..7]
- demo-data.demo_entries[0..7]
- demo-data.demo_entries[0..7]
- demo-data.demo_entries[0..7]
- demo-data.demo_entries[0..7]

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
- [ ] **Archetype honored:** the layout follows the "index_list" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

Anchored by the earth-green #B2D188 on license badges and the back-arrow, the screen stays refined and balanced in its acknowledgment of open-source foundations.

↑↑↑ MOCKUP PROMPT
