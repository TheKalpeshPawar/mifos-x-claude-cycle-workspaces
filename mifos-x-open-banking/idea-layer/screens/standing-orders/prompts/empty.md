---
ui_yaml_sha: 993761900d60ef7be1f81c63930e46c519c3c997ab0e078c4e378490b32f227c
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 653ecfd3e8e8c2e0905476dad5bbdfc905be758962cebbca53b832183d0a9c8e

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: standing-orders
state: empty
state_visibility: empty

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# standing-orders — empty state

> Auto-generated from screens/standing-orders/ui.yaml @ SHA 4bb8a2f82af9bae4
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the empty state of the Standing Orders screen for **HSBC Open Banking**, a UK Open Banking AISP app where OBReadStandingOrder6 returns no recurring payment records for the selected account.

Palette: primary #95CDF7, surface #101417, onSurface #E0E3E8, onSurfaceVariant #C1C7CE, surfaceContainer #1C2024, outline #8B9198, secondary #B7C9D9, surfaceVariant #41474D, primaryContainer #004B6F, onPrimary #00344E

**Component 1 - Top App Bar** (56dp, 393dp wide): back-arrow icon in #95CDF7, title "Standing Orders" Outfit Medium 22sp #E0E3E8, container #101417, empty_state archetype.

**Component 2 - Stat Block** (40dp, 361dp wide): label "0 Active · 0 Inactive" Outfit Medium 14sp #8B9198 aligned start to signal zero-state, 12dp top padding.

**Component 3 - Empty State** (centered in remaining height, 361dp wide): icon "autorenew" 64dp #C1C7CE centered, headline "No standing orders" Outfit Medium 20sp #E0E3E8 centered, body text "Scheduled recurring payments from your HSBC account will appear here" Outfit Regular 14sp #C1C7CE centered, 24dp gap between illustration, headline and body, generous vertical breathing room.

**Component 4 - Bottom Navigation Bar** (80dp, 393dp wide): container #1C2024, active tab #95CDF7, inactive tabs #8B9198.

Do not use em-dash in the headline or body text. Do not render phantom card skeletons or shimmer rows in this empty state. Do not add a "Set up standing order" or "Schedule payment" button; this AISP screen can never initiate payments. Do not break the dark #101417 background with a bright or white illustration panel.

The empty screen reads as calm: the "autorenew" icon in #C1C7CE and Trust Blue #95CDF7 navigation anchor tell the customer clearly that no recurring payments are scheduled, without visual alarm.

↑↑↑ MOCKUP PROMPT
