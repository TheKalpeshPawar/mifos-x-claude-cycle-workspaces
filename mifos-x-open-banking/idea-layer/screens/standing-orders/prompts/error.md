---
ui_yaml_sha: 993761900d60ef7be1f81c63930e46c519c3c997ab0e078c4e378490b32f227c
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 36b2b7534de111d6d7830b4e3e772fc357931de652a79385b013884627a272ed

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: standing-orders
state: error
state_visibility: error

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# standing-orders — error state

> Auto-generated from screens/standing-orders/ui.yaml @ SHA 2b9cc02c8342d971
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the error state of the Standing Orders screen for **HSBC Open Banking**, a UK Open Banking AISP app where the OBReadStandingOrder6 API request has failed and the customer sees a clear recovery path.

Palette: primary #95CDF7, onPrimary #00344E, surface #101417, onSurface #E0E3E8, onSurfaceVariant #C1C7CE, error #FFB4AB, errorContainer #93000A, onErrorContainer #FFDAD6, surfaceContainer #1C2024, outline #8B9198

**Component 1 - Top App Bar** (56dp, 393dp wide): back-arrow icon in #95CDF7, title "Standing Orders" Outfit Medium 22sp #E0E3E8, container #101417, error_state archetype.

**Component 2 - Error State** (centered in remaining 716dp, 361dp wide): cloud-off icon 64dp #FFB4AB centered, headline "Could not load standing orders" Outfit Medium 20sp #E0E3E8 centered, supporting text "Check your connection and try again" Outfit Regular 14sp #C1C7CE centered, 24dp gap between elements, generous vertical breathing room.

**Component 3 - Button** (48dp tall, 240dp wide, centered): filled container #95CDF7, label "Try again" Outfit Medium 14sp #00344E, radius 24dp, 24dp below Error State.

**Component 4 - Bottom Navigation Bar** (80dp, 393dp wide): container #1C2024, active tab #95CDF7, inactive tabs #8B9198.

Do not use em-dash in the error headline, supporting text, or button label. Do not show card skeletons or partial list rows behind the error message. Do not color the retry button in error red; #93000A is reserved for destructive-action containers only. Do not add a secondary CTA or floating action button that could imply payment scheduling capability.

The error screen reads as restrained: a single #FFB4AB failure icon and Trust Blue #95CDF7 retry button handle the API failure without visual noise, aligned with the calm regulated-finance design system.

↑↑↑ MOCKUP PROMPT
