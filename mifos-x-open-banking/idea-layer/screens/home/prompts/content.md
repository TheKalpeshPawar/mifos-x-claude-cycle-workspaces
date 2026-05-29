---
ui_yaml_sha: b89d839e6c9e3be9d2a9ef40cf53bd6b62a21124885037343b404ee39dd8d76d
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 82418c61623a94e83e07736e5b8b71c568501b572e100b802a8d4624be8bc455

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: dashboard

feature: home
state: content
state_visibility: content

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# home — content state

> Auto-generated from screens/home/ui.yaml @ SHA 39c82f1bfadd4407
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the home screen for **Mifos X Open Banking**, a Open Banking KMP super-app for consumer retail banking and field officer agent banking in emerging markets.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, error #FFB4AB, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, outline #8F9285, pending #E8A317.

**Component 1 — App Bar** (full width, 56dp tall): Greeting "Good morning, Alex" Outfit SemiBold 18sp #E3E3D8 left-aligned 16dp padding. Date "Monday, 25 May 2026" Outfit Regular 12sp #C5C8BA below greeting. Background #12140E. Zero elevation.

**Component 2 — Card** (full width minus 32dp insets, top margin 16dp, 16dp corner radius, background #354E16, 20dp padding): Primary account card. Label "Primary Checking" Outfit Regular 12sp #CDEDA3. Balance "£4,250.00" Outfit SemiBold 28sp #E3E3D8 top margin 4dp. IBAN "•••• •••• •••• 0130" Outfit Regular 12sp #A0CFCB top margin 4dp. Row of 3 Chip Row items top margin 16dp each filled #1F4E4B 32dp tall 8dp padding: "Send Money" Outfit Medium 13sp #BCEBE7, "Beneficiaries" same, "View Cards" same. dashboard archetype.

**Component 3 — Card** (full width minus 32dp insets, top margin 12dp, 12dp corner radius, background #1E201A, 12dp padding): Balance chip row. Wallet icon 20dp #B2D188. Text "Total across 3 accounts: £12,480.50" Outfit Regular 14sp #E3E3D8.

**Component 4 — List Row** (full width minus 32dp insets, top margin 24dp): Section row header "Recent Transactions" Outfit SemiBold 14sp #E3E3D8 left, "View All" Outfit Medium 14sp #B2D188 right. Three transaction rows each 64dp tall with 1dp divider #44483D. Row 1: shopping_cart icon 40dp background #282A24, "Tesco Supermarket" Outfit Medium 14sp #E3E3D8, "23 May 2026 · Groceries" Outfit Regular 12sp #C5C8BA, amount "-£42.50" Outfit Medium 14sp #FFB4AB, badge "DEBIT" Outfit Regular 11sp #FFB4AB. Row 2: payments icon, "Salary Payment", "22 May 2026 · Income", "+£3,200.00" Outfit Medium 14sp #B2D188, badge "CREDIT" Outfit Regular 11sp #B2D188. Row 3: bolt icon, "EDF Energy", "20 May 2026 · Utilities", "-£94.20" #FFB4AB, badge "DEBIT".

**Component 5 — Grid** (full width minus 32dp insets, top margin 24dp, 2-column grid 12dp gap): Section title "Services" Outfit SemiBold 14sp #E3E3D8. Three service Cards each 80dp tall 12dp corner radius background #1E201A centered icon 24dp #A0CFCB and label below: "Standing Orders" Outfit Regular 12sp #C5C8BA, "ATM & Branches", "FX Rates".

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Full scrollable layout on #12140E. The earth-green #B2D188 on credit amounts and the "View All" link anchors positive financial moments with warmth and growth energy calibrated to the trust-first banking aesthetic.

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
- [ ] **Archetype honored:** the layout follows the "dashboard" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

Anchored by the earth-green #B2D188 on credit moments and quick-links, the home screen stays warm and balanced across all account states.

↑↑↑ MOCKUP PROMPT
