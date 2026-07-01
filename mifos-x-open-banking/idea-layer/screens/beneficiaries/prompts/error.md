---
ui_yaml_sha: d9ae9d4b46f8c880e1bdab3fb08cc6bf8df99140964c3c5557cba8f389363eda
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 298beb42c393ba4c8afa73bccc1684d2425f2044f795f37a11d9ca5dc90f6187

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: beneficiaries
state: error
state_visibility: error

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# beneficiaries — error state

> Auto-generated from screens/beneficiaries/ui.yaml @ SHA ea2da94e79bc92c1
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the error state of the Beneficiaries screen for **HSBC Open Banking**, a UK Open Banking AISP app where the OBReadBeneficiary5 request has failed and the customer needs a clear, non-alarming recovery path.

Palette: primary #95CDF7, onPrimary #00344E, surface #101417, onSurface #E0E3E8, onSurfaceVariant #C1C7CE, error #FFB4AB, errorContainer #93000A, onErrorContainer #FFDAD6, surfaceContainer #1C2024, outline #8B9198

**Component 1 - Top App Bar** (56dp, 393dp wide): back-arrow icon in #95CDF7, title "Beneficiaries" Outfit Medium 22sp #E0E3E8, container #101417, error_state archetype.

**Component 2 - Error State** (centered in remaining 716dp, 361dp wide): cloud-off icon 64dp #FFB4AB centered, headline "Could not load payees" Outfit Medium 20sp #E0E3E8 centered, supporting text "Check your connection and try again" Outfit Regular 14sp #C1C7CE centered, 24dp gap between elements, generous vertical breathing room above and below.

**Component 3 - Button** (48dp tall, 240dp wide, centered): filled style, container #95CDF7, label "Try again" Outfit Medium 14sp #00344E, radius 24dp, positioned 24dp below Error State.

**Component 4 - Button** (48dp tall, 240dp wide, centered): outlined style, border 1dp #8B9198, label "View consents" Outfit Medium 14sp #95CDF7, radius 24dp, 12dp gap below filled button, for users needing to re-authorise.

**Component 5 - Bottom Navigation Bar** (80dp, 393dp wide): container #1C2024, active tab #95CDF7, inactive tabs #8B9198.

Do not use em-dash in error messages or button labels. Do not show partial list rows or skeleton cards behind the error message. Do not paint the primary retry button in error red #93000A; the action is affirmative, not destructive. Do not add a floating action button or secondary CTA that implies payment initiation.

The error screen reads as restrained: a single #FFB4AB cloud-off icon and Trust Blue #95CDF7 retry button resolve the failed payee fetch without visual drama, holding the regulated-finance tone.

↑↑↑ MOCKUP PROMPT
