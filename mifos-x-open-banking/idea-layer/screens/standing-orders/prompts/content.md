---
ui_yaml_sha: 993761900d60ef7be1f81c63930e46c519c3c997ab0e078c4e378490b32f227c
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 15bf8b519a61d683df7d656074e33ac2f272751b2927caf167b2e6bba11d085e

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: standing-orders
state: content
state_visibility: content

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# standing-orders — content state

> Auto-generated from screens/standing-orders/ui.yaml @ SHA 210568bdc67ec75a
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the Standing Orders screen for **HSBC Open Banking**, a UK Open Banking AISP app presenting five customer-scheduled recurring payments from OBReadStandingOrder6 in a read-only AISP view.

Palette: primary #95CDF7, onPrimary #00344E, surface #101417, onSurface #E0E3E8, onSurfaceVariant #C1C7CE, surfaceContainer #1C2024, secondary #B7C9D9, outline #8B9198, error #FFB4AB, primaryContainer #004B6F

**Component 1 - Top App Bar** (56dp, 393dp wide): back-arrow icon in #95CDF7, title "Standing Orders" Outfit Medium 22sp #E0E3E8, container #101417, detail_screen archetype.

**Component 2 - Stat Block** (40dp, 361dp wide): summary label "4 Active · 1 Inactive" Outfit Medium 14sp #C1C7CE aligned start, 12dp top padding.

**Component 3 - List** (scrollable, remaining height, 361dp wide): five Cards stacked with 12dp gap and 16dp horizontal insets. Card A (SO-001): container #1C2024 radius 12dp, status badge "Active" background #004B6F label #95CDF7 Outfit Medium 12sp, headline "Jameson Lettings" Outfit Medium 16sp #E0E3E8, amount "GBP 1,200.00" Outfit Regular 14sp #FFB4AB, frequency "Monthly on the 1st · Next 1 Jul 2026" Outfit Regular 13sp #C1C7CE, footer "Ref RENT-FLAT12 · 40-12-09 65872310" Outfit Regular 12sp #8B9198. Card B (SO-002): badge "Active" #004B6F / #95CDF7, headline "ISA Saver" #E0E3E8, amount "GBP 200.00" #FFB4AB, frequency "Monthly on the 1st · Next 1 Jul 2026" #C1C7CE, footer "Ref ISA-TOPUP · 60-16-13 31926819" #8B9198. Card C (SO-003): badge "Active" #004B6F / #95CDF7, headline "PureGym" #E0E3E8, amount "GBP 24.99" #FFB4AB, frequency "Monthly on the 15th · Next 15 Jul 2026" #C1C7CE, footer "Ref GYM-MBR · 20-00-00 55512345" #8B9198. Card D (SO-004): badge "Inactive" container #41474D label #C1C7CE, headline "Oxfam GB" #E0E3E8, amount "GBP 10.00" #C1C7CE muted as mandate is cancelled, date "Final payment 28 Dec 2025" Outfit Regular 13sp #8B9198, footer "Ref CHARITY-DON · 08-60-01 20321982" #8B9198. Card E (SO-005): badge "Active" #004B6F / #95CDF7, headline "Marcus Savings" #E0E3E8, amount "GBP 50.00" #FFB4AB, frequency "Weekly every Friday · Next 4 Jul 2026" #C1C7CE, footer "Final 25 Dec 2026 · Ref SAVINGS-SWEEP" #8B9198.

**Component 4 - Bottom Navigation Bar** (80dp, 393dp wide): container #1C2024, active tab #95CDF7, inactive tabs #8B9198.

Do not use em-dash in any card label, amount field, or frequency description. Do not show a Cancel or Modify button on any card; this is a read-only mandate registry. Do not render Oxfam GB card in error red; the mandate has simply completed its term. Do not break the dark card theme with a white or light-background card container.

The standing-orders roster reads as calm: five mandate cards with amounts in #FFB4AB and Active badges in Trust Blue #95CDF7 give an immediate, data-legible picture on the near-black surface.

↑↑↑ MOCKUP PROMPT
