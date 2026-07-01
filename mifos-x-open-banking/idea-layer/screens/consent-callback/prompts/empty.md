---
ui_yaml_sha: 89368ce68522a27b426af78efafaade84222dfd7246d861a644ffa9b3030c8b6
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 7bd5c1ad9d23a7a6f340e07846e09c86995edba1679386eee836dcbefcbeebb3

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: consent-callback
state: empty
state_visibility: empty

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# consent-callback — empty state

> Auto-generated from screens/consent-callback/ui.yaml @ SHA f72f1318818c47f9
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the empty state of the consent-callback screen for **HSBC Open Banking**, a UK AISP app awaiting a polling confirmation after the PSU returned from the HSBC portal without a completed authorisation response, built on Trust Blue minimalist Material 3 DARK on 393x852dp Pixel 5.

Palette: surface #101417, onSurface #E0E3E8, primary #95CDF7, onPrimary #00344E, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, primaryContainer #004B6F

**Component 1 - Top App Bar** (full-width, 64dp): Outfit Medium 20sp "Connecting HSBC" #E0E3E8 on #101417; no back-arrow; no trailing actions; archetype empty_state.

**Component 2 - Empty State** (centred, full-width minus 32dp, 300dp vertical): pending icon 72dp #C1C7CE centred; Outfit Medium 22sp headline "Awaiting confirmation" #E0E3E8 centred; 8dp gap; Outfit Regular 14sp "We have not yet received your authorisation from HSBC. This may take a few moments." #C1C7CE centred; 16dp gap below.

**Component 3 - Button** (full-width minus 32dp, 48dp): filled "Check again" Outfit Medium 14sp #00344E on #95CDF7 container radius 24dp; centred 24dp below body.

**Component 4 - Button** (full-width minus 32dp, 48dp): text button "Cancel" Outfit Medium 14sp #C1C7CE radius 24dp; 8dp gap below first button; returns PSU to home screen.

Do not use em-dash anywhere in labels or body copy. Do not make any headline longer than 3 lines or any subtitle longer than 25 words. Do not break the dark #101417 surface theme between sections by introducing light containers or white backgrounds. Do not place light-coloured text on a light-coloured button, or dark text on a dark button.

No bottom navigation bar on this transient OAuth landing; the pending icon in muted #C1C7CE reflects uncertainty without alarm, and Trust Blue (#95CDF7) on "Check again" gives the PSU restrained control while the AISP polls for the HSBC authorisation outcome.

↑↑↑ MOCKUP PROMPT
