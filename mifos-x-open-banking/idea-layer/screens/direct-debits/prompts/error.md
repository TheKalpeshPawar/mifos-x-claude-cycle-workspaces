---
ui_yaml_sha: 8f627a0862016e34b232d8c97c47bf23a2cebbe6255b04b8f9e6429b85a1f5c9
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 1b4516ad2ce235c66451c06cd8ff79e34841546ca6da3c3f4d506b2550e21eec

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: direct-debits
state: error
state_visibility: error

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# direct-debits — error state

> Auto-generated from screens/direct-debits/ui.yaml @ SHA 83c5a703eebf2500
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the error state of the Direct Debits screen for **HSBC Open Banking**, a UK Open Banking AISP app where the OBReadDirectDebit2 request has failed and the customer needs a clear recovery path.

Palette: primary #95CDF7, onPrimary #00344E, surface #101417, onSurface #E0E3E8, onSurfaceVariant #C1C7CE, error #FFB4AB, errorContainer #93000A, onErrorContainer #FFDAD6, surfaceContainer #1C2024, outline #8B9198

**Component 1 - Top App Bar** (56dp, 393dp wide): back-arrow icon in #95CDF7, title "Direct Debits" Outfit Medium 22sp #E0E3E8, container #101417, error_state archetype.

**Component 2 - Error State** (centered in remaining 716dp, 361dp wide): cloud-off icon 64dp #FFB4AB centered, headline "Could not load mandates" Outfit Medium 20sp #E0E3E8 centered, supporting text "No network connection. Check your connection and retry." Outfit Regular 14sp #C1C7CE centered, 24dp gap between elements, generous vertical breathing room.

**Component 3 - Button** (48dp tall, 240dp wide, centered): filled container #95CDF7, label "Try again" Outfit Medium 14sp #00344E, radius 24dp, 24dp below Error State, retries the OBReadDirectDebit2 call.

**Component 4 - Button** (48dp tall, 240dp wide, centered): outlined border 1dp #8B9198, label "View consents" Outfit Medium 14sp #95CDF7, radius 24dp, 12dp below primary button, links to consent-list screen for ConsentRevoked failures.

**Component 5 - Bottom Navigation Bar** (80dp, 393dp wide): container #1C2024, active tab #95CDF7, inactive tabs #8B9198.

Do not use em-dash in error copy or button labels. Do not display partial mandate cards behind the error overlay. Do not color the primary retry button in error red; #93000A is reserved for destructive container tinting only. Do not add any payment-mandate creation affordance that implies direct debit setup capability.

The error screen reads as restrained: a #FFB4AB failure icon and Trust Blue #95CDF7 retry button handle the mandate fetch failure without drama, preserving the calm regulated-finance aesthetic.

↑↑↑ MOCKUP PROMPT
