---
ui_yaml_sha: 0d92768a4d5ddf82143347d12811e4d5c43b46201bead5239e2c5443c0a89f3b
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: c8ac0989fcac76659e2248c73157bd0d5ec5f93a109431098747014f43933c12

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: consumer-home
state: content
state_visibility: content

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# consumer-home — content state

> Auto-generated from screens/consumer-home/ui.yaml @ SHA 0bde566f2547a653
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the consumer home screen for **Mifos X Open Banking**, a professional open banking KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, secondary #A0CFCB, error #FFB4AB, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317.

**Component 1 — App Bar** (56dp tall, full width, background #12140E): Left side "Good morning, Alex" Outfit SemiBold 20sp #E3E3D8. Right side notification bell icon 24dp #C5C8BA.

**Component 2 — Card** (balance card, full width minus 32dp insets, 16dp corner radius, background #1E201A, top margin 16dp): Label "Total Balance" Outfit Regular 13sp #C5C8BA. Amount "£4,250.00" Outfit Bold 32sp #B2D188. Chip "Primary Checking" 24dp tall pill background #354E16 Outfit Medium 12sp #CDEDA3 top margin 8dp. Divider 1dp #44483D top margin 12dp. Below divider: two columns "Income this month / + £3,200.00" and "Spent this month / - £1,840.00" each Outfit Regular 12sp label #C5C8BA and Outfit SemiBold 14sp amount.

**Component 3 — Chip Row** (quick actions, full width minus 32dp insets, top margin 20dp): 4 chips horizontal "Send Money", "Accounts", "Standing Orders", "Cards" each 36dp tall 16dp corner radius background #1E201A outline 1dp #44483D Outfit Medium 12sp #E3E3D8, 8dp gap.

**Component 4 — List Row** section header (full width minus 32dp insets, top margin 20dp): "Recent Transactions" Outfit SemiBold 16sp #E3E3D8 left, "See all" Outfit Medium 13sp #B2D188 right.

**Component 5 — List Row** (transaction 1, full width minus 32dp insets, 56dp tall, background #1E201A 8dp corner radius): "Coffee Shop" Outfit Regular 14sp #E3E3D8 left, "- £3.50" Outfit SemiBold 14sp #FFB4AB right.

**Component 6 — List Row** (transaction 2, same style): "Salary" Outfit Regular 14sp #E3E3D8, "+ £3,200.00" Outfit SemiBold 14sp #B2D188.

**Component 7 — List Row** (transaction 3, same style): "Supermarket" Outfit Regular 14sp #E3E3D8, "- £42.80" Outfit SemiBold 14sp #FFB4AB.

**Component 8 — Button** (full width minus 32dp insets, 48dp tall, top margin 16dp, outlined 1dp #44483D, 8dp corner radius, label "View All Transactions" Outfit Medium 14sp #E3E3D8).

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Scrollable layout on #12140E. The sage-green #B2D188 on the balance amount and income figures signals financial health and growth, projecting calm stability and trustworthy confidence calibrated to the taste-default aesthetic.

↑↑↑ MOCKUP PROMPT
