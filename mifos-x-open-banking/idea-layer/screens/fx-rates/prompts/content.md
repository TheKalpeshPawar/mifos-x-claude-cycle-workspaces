---
ui_yaml_sha: 5b4e63fd968d1623f04fb68f35f8d1f64c6a5215034b56bce2efabe7cb563790
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: ab1435e0c620d39e24d6c00a0f1ae1ecaeb17e941c526d12ddb369a16794a0c5

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: fx-rates
state: content
state_visibility: content

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# fx-rates — content state

> Auto-generated from screens/fx-rates/ui.yaml @ SHA c6a5160d963c101c
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the fx-rates screen for **Mifos X Open Banking**, a Open Banking KMP super-app for consumer retail banking and field officer agent banking in emerging markets.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, error #FFB4AB, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, outline #8F9285, pending #E8A317.

**Component 1 — App Bar** (full width, 56dp tall): Title "Exchange Rates" Outfit Medium 18sp #E3E3D8 centered. Background #12140E. Subtitle "Rates updated: 14 May 2026, 15:42 UTC" Outfit Regular 12sp #8F9285 below title centered.

**Component 2 — Card** (full width minus 32dp insets, top margin 16dp, 16dp corner radius, background #1E201A, 16dp padding): Converter card. Text Field "I want to send" labeled Outfit Regular 12sp #8F9285, value "1,000" Outfit Medium 16sp #E3E3D8, currency pill "GBP" Outfit Medium 14sp #CDEDA3 filled #354E16 right side. Swap icon 24dp #A0CFCB centered with 12dp margin. Text Field "To" labeled same style, value "EUR" currency pill same style. Result "= 1,167.20 EUR" Outfit SemiBold 24sp #B2D188 centered with 12dp top margin. Rate info "Rate: 1 GBP = 1.1672 EUR" Outfit Regular 12sp #8F9285 centered. Button "Send this amount" Outfit SemiBold 16sp #1F3701 filled #B2D188 48dp tall 999dp radius full width minus 16dp insets top margin 16dp.

**Component 3 — Bottom Nav** (1dp divider #44483D, top margin 24dp, left-aligned label "Popular Pairs" Outfit SemiBold 14sp #E3E3D8 with 16dp padding).

**Component 4 — List Row** (full width minus 32dp insets): 6 rate rows each 56dp tall with 1dp divider #44483D between rows. Each row: currency pair label left "GBP / EUR" Outfit Medium 14sp #E3E3D8, rate value center "1.1672" Outfit Regular 14sp #C5C8BA, change badge right "+0.2%" Outfit Medium 12sp #B2D188 for positive and "-0.1%" Outfit Medium 12sp #FFB4AB for negative. Rows in order: GBP/EUR 1.1672 +0.2%, GBP/USD 1.2834 -0.1%, GBP/JPY 193.45 +0.4%, EUR/USD 1.0993 -0.3%, USD/INR 83.22 0.0%, EUR/GBP 0.8568 -0.2%.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Full scrollable layout on #12140E. The soft earth-green #B2D188 on the CTA button and positive rate changes communicates financial growth with calm, balanced confidence appropriate to a regulated open banking context.

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

Anchored by the CTA accent #B2D188 and rate-change highlights, the exchange rates screen stays calm and balanced for regulated open banking.

↑↑↑ MOCKUP PROMPT
