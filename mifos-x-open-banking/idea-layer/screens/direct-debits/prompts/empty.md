---
ui_yaml_sha: 8f627a0862016e34b232d8c97c47bf23a2cebbe6255b04b8f9e6429b85a1f5c9
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: e3e87de3ecc2631c8e4c47c3b46dc9b681181d9f64012ee94221b6856806c851

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: direct-debits
state: empty
state_visibility: empty

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# direct-debits — empty state

> Auto-generated from screens/direct-debits/ui.yaml @ SHA fd955443e82e07b3
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the empty state of the Direct Debits screen for **HSBC Open Banking**, a UK Open Banking AISP app where OBReadDirectDebit2 returns no mandate records for the selected HSBC account.

Palette: primary #95CDF7, surface #101417, onSurface #E0E3E8, onSurfaceVariant #C1C7CE, surfaceContainer #1C2024, outline #8B9198, secondary #B7C9D9, surfaceVariant #41474D, primaryContainer #004B6F, onPrimary #00344E

**Component 1 - Top App Bar** (56dp, 393dp wide): back-arrow icon in #95CDF7, title "Direct Debits" Outfit Medium 22sp #E0E3E8, container #101417, empty_state archetype.

**Component 2 - Chip Row** (48dp, 361dp wide): chips displaying "0 Active" and "0 Inactive" both with outlined border 1dp #41474D and label #8B9198 Outfit Medium 13sp, indicating no mandates, read-only display.

**Component 3 - Empty State** (centered in remaining height, 361dp wide): icon "subscriptions" 64dp #C1C7CE centered, headline "No direct debits" Outfit Medium 20sp #E0E3E8 centered, body text "Direct debit mandates on your HSBC account will appear here when active" Outfit Regular 14sp #C1C7CE centered, 24dp gap between elements, generous vertical breathing room.

**Component 4 - Bottom Navigation Bar** (80dp, 393dp wide): container #1C2024, active tab #95CDF7, inactive tabs #8B9198.

Do not use em-dash in the headline or body copy. Do not render phantom card skeletons or shimmer rows in this empty state. Do not add a "Set up direct debit" or payment-mandate CTA; this AISP screen has no payment-initiation capability. Do not break the dark #101417 background with a white or light illustration panel.

The empty screen reads as calm: the "subscriptions" icon in #C1C7CE on the dark surface communicates no active mandates clearly, with Trust Blue #95CDF7 reserved for the navigation anchor.

↑↑↑ MOCKUP PROMPT
