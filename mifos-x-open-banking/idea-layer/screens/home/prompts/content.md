---
ui_yaml_sha: a574db0835367d71b15650135b39b1420d4c79ed53118ef031635df642260620
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

> Auto-generated from screens/home/ui.yaml @ SHA 0a8d8789e95dcb3c
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the **content** state of the Home screen for **Mifos X Open Banking**, a open banking KMP super-app delivering consumer retail banking and field officer agent banking powered by Open Bank Project API v7 across Android, iOS, Desktop, and Web.

Palette: background #12140E, surface #12140E, onSurface #E3E3D8, primary #B2D188, onPrimary #1F3701, primaryContainer #354E16, onPrimaryContainer #CDEDA3, secondary #A0CFCB, onSecondary #003735, secondaryContainer #1F4E4B, surfaceContainer #1E201A, surfaceContainerHigh #282A24, outline #8F9285, outlineVariant #44483D, onSurfaceVariant #C5C8BA, error #FFB4AB, pending #E8A317, navActiveIndicator #354E16.

**Component 1 - Greeting Text** (full width minus 32dp insets, top margin 24dp): "Good morning, Alex." Outfit SemiBold 22sp #E3E3D8, left-aligned. No background. Baseline sits 24dp below the status bar.

**Component 2 - Greeting Date** (full width minus 32dp insets, top margin 4dp): "Wednesday, 28 May 2026" Outfit Regular 13sp #C5C8BA, left-aligned. Zero background, single line.

**Component 3 - Primary Account Card** (full width minus 32dp insets, 148dp tall, 16dp corner radius, top margin 20dp): dashboard hero card. Background #1E201A, 1dp border #44483D. Left column: label "Main Savings Account" Outfit Medium 12sp #C5C8BA; account number "GHS - 1002345678" Outfit Regular 11sp #8F9285, top margin 4dp; balance label "Available Balance" Outfit Regular 11sp #C5C8BA, top margin 16dp; balance amount "GHS 4,250.00" Outfit Bold 28sp #B2D188. Right column, top-right corner: 40dp circular avatar filled #354E16 with initials "AO" Outfit SemiBold 16sp #CDEDA3. Bottom row, top margin 16dp: four 68dp-wide action chips (pill radius, 32dp tall, filled #282A24 with 1dp border #44483D each): "Transfer" Outfit Medium 12sp #E3E3D8, "Pay Bill" Outfit Medium 12sp #E3E3D8, "Top-up" Outfit Medium 12sp #E3E3D8, "More" Outfit Medium 12sp #C5C8BA. Gap between chips 8dp.

**Component 4 - Total Balance Chip** (full width minus 32dp insets, 48dp tall, 12dp corner radius, top margin 12dp): single wide pill card background #282A24. Left: label "Total Portfolio" Outfit Regular 12sp #C5C8BA; right-aligned total "GHS 11,890.50" Outfit SemiBold 15sp #B2D188. Right edge: chevron-right icon 18dp tinted #8F9285. Vertically centered content with 16dp horizontal padding.

**Component 5 - Recent Transactions Header** (full width minus 32dp insets, 40dp tall, top margin 24dp): horizontal Stack. Left: "Recent Transactions" Outfit SemiBold 16sp #E3E3D8. Right: text button "See All" Outfit Medium 13sp #B2D188 with data-nav-to="transactions". Aligned baseline, space-between layout.

**Component 6 - Transaction Row 1** (full width minus 32dp insets, 64dp tall, 12dp corner radius, top margin 8dp): card background #1E201A, 1dp border #44483D. Leading 40dp circle icon container background #354E16 with upward-arrow icon 20dp tinted #CDEDA3. Center column: primary label "Mobile Top-up - Vodafone" Outfit Medium 14sp #E3E3D8; secondary label "Today, 08:42" Outfit Regular 12sp #8F9285. Trailing amount "-GHS 42.50" Outfit SemiBold 14sp #FFB4AB, right-aligned. 16dp horizontal padding, vertically centered rows.

**Component 7 - Transaction Row 2** (full width minus 32dp insets, 64dp tall, 12dp corner radius, top margin 8dp): card background #1E201A, 1dp border #44483D. Leading 40dp circle icon container background #1F4E4B with downward-arrow icon 20dp tinted #A0CFCB. Center column: primary label "Salary Credit - MBS Corp" Outfit Medium 14sp #E3E3D8; secondary label "Yesterday, 17:15" Outfit Regular 12sp #8F9285. Trailing amount "+GHS 3,200.00" Outfit SemiBold 14sp #B2D188, right-aligned. 16dp horizontal padding, vertically centered rows.

**Component 8 - Transaction Row 3** (full width minus 32dp insets, 64dp tall, 12dp corner radius, top margin 8dp): card background #1E201A, 1dp border #44483D. Leading 40dp circle icon container background #44483D with transfer icon 20dp tinted #C5C8BA. Center column: primary label "Transfer to James Asante" Outfit Medium 14sp #E3E3D8; secondary label "27 May, 14:03" Outfit Regular 12sp #8F9285. Trailing amount "-GHS 500.00" Outfit SemiBold 14sp #FFB4AB, right-aligned. Trailing right edge: status badge 6dp filled circle #E8A317 indicating pending state, vertically centered. 16dp horizontal padding.

**Component 9 - Services Section Title** (full width minus 32dp insets, 40dp tall, top margin 24dp): "Banking Services" Outfit SemiBold 16sp #E3E3D8, left-aligned, vertically centered.

**Component 10 - Services Grid** (full width minus 32dp insets, top margin 8dp, 2x3 grid with 12dp gaps): six service tile cards each 88dp tall, 12dp corner radius, background #1E201A, 1dp border #44483D. Each tile: centered icon 28dp tinted #B2D188 at top-center with 16dp top padding, label Outfit Medium 12sp #C5C8BA centered below with 8dp top gap. Tiles in order: (1) icon bank-outline, label "Accounts"; (2) icon repeat-arrows, label "Transfers"; (3) icon document-text, label "Statements"; (4) icon credit-card, label "Cards"; (5) icon location-marker, label "Find ATM"; (6) icon headset, label "Support". All labels single-line.

**Component 11 - Bottom Spacer** (full width, 80dp tall): transparent spacer providing clearance above the bottom navigation bar so final grid row is not clipped on scroll.

**Component 12 - Bottom Navigation** (full width, 64dp tall, anchored bottom): 5 tabs: "Home" (selected, indicator pill #354E16 48dp wide 32dp tall, icon 24dp tinted #B2D188, label Outfit Medium 11sp #B2D188), "Accounts" (icon 24dp tinted #8F9285, label Outfit Regular 11sp #8F9285), "Transfers" (icon 24dp tinted #8F9285, label Outfit Regular 11sp #8F9285), "Loans" (icon 24dp tinted #8F9285, label Outfit Regular 11sp #8F9285), "Profile" (icon 24dp tinted #8F9285, label Outfit Regular 11sp #8F9285). Background #1E201A, top divider 1dp #44483D. Tab width equal-distributed.

DO NOT use em-dash anywhere in text. DO NOT make any headline more than 3 lines or any subtitle more than 25 words. DO NOT break the page theme between sections. DO NOT place light text on light buttons or dark text on dark buttons.

The earth-green primary #B2D188 anchors every trust signal - selected navigation, positive transaction amounts, account balance display, and service tile icons - building a calm, professional financial tone that communicates stability without austerity. Generous 24dp section breaks and #1E201A card surfaces lift content off the near-black background, giving the dashboard a structured, breathable density calibrated for daily financial monitoring by both retail consumers and field officers.

↑↑↑ MOCKUP PROMPT
