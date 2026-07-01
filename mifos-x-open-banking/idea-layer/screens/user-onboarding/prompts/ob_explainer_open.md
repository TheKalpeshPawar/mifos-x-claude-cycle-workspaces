---
ui_yaml_sha: 927a4ea2aa924d185dec8870cbdfc9f4ac91b01311daef7f791259aeb739a5f9
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 60e886cd04e333a553eff28786ae21c0680817b31e1254fd093bf4c09bb4f393

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: user-onboarding
state: ob_explainer_open
state_visibility: ob_explainer_open

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# user-onboarding — ob_explainer_open state

> Auto-generated from screens/user-onboarding/ui.yaml @ SHA 9bbd6b66ab13b7ed
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the ob_explainer_open state of the User Onboarding screen for **HSBC Open Banking**, a UK account-information app that overlays a bottom sheet explaining the Open Banking mechanism while the consent_explainer step is dimmed below.

Palette: primary #95CDF7, onPrimary #00344E, primaryContainer #004B6F, onPrimaryContainer #C9E6FF, surface #101417, onSurface #E0E3E8, surfaceContainerHighest #313539, onSurfaceVariant #C1C7CE

**Component 1 - Card** (393dp wide, full height): Background layer showing the consent_explainer detail_screen step: "What we never do" section header and three reassurance rows, dimmed by a scrim #000000 at 40% opacity. The background is visible but not interactive.

**Component 2 - Card** (393dp wide, 420dp tall, surfaceContainerHighest #313539, 28dp top radius, 0dp bottom radius, anchored to screen bottom): Bottom sheet for the Open Banking explainer. Drag handle: 32dp wide 4dp tall rect in outline #8B9198, centred 8dp from top. Outfit 20sp bold "How Open Banking works" in onSurface #E0E3E8, 16dp below handle, left-aligned with 16dp padding.

**Component 3 - List** (361dp wide, 3 rows at 80dp each inside the sheet): Row 1: how_to_reg icon primary #95CDF7 24dp, "Register once" Outfit 16sp onSurface, "Create your profile here. No HSBC credentials needed in this app." Outfit 13sp onSurfaceVariant #C1C7CE. Row 2: login icon primary #95CDF7, "Approve on HSBC" Outfit 16sp onSurface, "Log in on HSBC's secure site and grant read-only access." Outfit 13sp onSurfaceVariant. Row 3: shield icon primary #95CDF7, "Data flows securely" Outfit 16sp onSurface, "HSBC sends your account data over encrypted FAPI 2.0 channels." Outfit 13sp onSurfaceVariant.

**Component 4 - Banner** (361dp wide, 56dp, primaryContainer #004B6F, 8dp radius): Outfit 14sp "You can revoke access at any time from Consents. HSBC also lets you revoke from their app." in onPrimaryContainer #C9E6FF.

**Component 5 - Button** (361dp wide, 48dp tall, primary #95CDF7 fill, onPrimary #00344E label, 999dp radius): "Close" Outfit 16sp bold. Anchored 16dp from sheet bottom edge. Closes the sheet and returns to consent_explainer.

DO NOT use em-dash anywhere in text. DO NOT make any headline longer than 3 lines or any subtitle longer than 25 words. DO NOT break the dark theme between sections. DO NOT place light-on-light or dark-on-dark text and button combinations.

The bottom sheet clarifies Open Banking in three plain steps, using #95CDF7 on each step icon to pull the eye through a balanced and reassuring narrative before the user taps Close and proceeds to connect HSBC.

↑↑↑ MOCKUP PROMPT
