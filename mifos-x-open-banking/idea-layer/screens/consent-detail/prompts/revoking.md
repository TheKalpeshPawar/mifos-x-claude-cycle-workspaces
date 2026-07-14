---
ui_yaml_sha: dc51a93dfe2c575708401b94ec0aad258941119f5f0891dc9bcbab82740013cd
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 18ce4f548677dbd1d3af2293349bec898d58abfc0569609c4ad6e620129a2eea

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: consent-detail
state: revoking
state_visibility: revoking

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# consent-detail — revoking state

> Auto-generated from screens/consent-detail/ui.yaml @ SHA 700f533ff8b773ff
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the revoking state of the consent-detail screen for **HSBC Open Banking**, a UK AISP app actively sending the DELETE consent request to the HSBC AIS API while blocking further interaction, built on Trust Blue minimalist Material 3 DARK on 393x852dp Pixel 5.

Palette: surface #101417, onSurface #E0E3E8, primary #95CDF7, onPrimary #00344E, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, primaryContainer #004B6F

**Component 1 - Top App Bar** (full-width, 64dp): Outfit Medium 22sp "Consent detail" #E0E3E8 on #101417; back-arrow leading disabled (non-interactive during revoke operation); archetype screen.

**Component 2 - Banner** (full-width minus 32dp, 56dp, #1C2024 radius 8dp): linear progress_indicator #95CDF7 track 4dp tall pinned to top of banner; Outfit Regular 14sp "Revoking HSBC access. Please wait..." #C1C7CE centred below indicator.

**Component 3 - Card** (full-width minus 32dp, 96dp, #1C2024 radius 12dp): HSBC logo 40dp circle at 0.6 opacity greyscale; Chip "Revoking..." outlined #8B9198 label #C1C7CE with circular progress_indicator 16dp inside chip right of label; "aac-fb2c4e8a-7d31-4c9e-9f2a-1b3c5d7e9f01" 12sp #8B9198 truncated.

**Component 4 - List** (full-width minus 32dp, opacity 0.4, non-interactive): "Data shared" section label 12sp #8B9198; 10 permission rows at reduced opacity showing check_circle_outline rows from the content state, visually signalling which access is being removed.

**Component 5 - Button** (full-width minus 32dp, 48dp): tonal "Revoke access" disabled state; container #313539 label #8B9198 radius 24dp; loading prevents re-tap.

Do not use em-dash anywhere in labels or body copy. Do not make any headline longer than 3 lines or any subtitle longer than 25 words. Do not break the dark #101417 surface theme between sections by introducing light containers or white backgrounds. Do not place light-coloured text on a light-coloured button, or dark text on a dark button.

The Trust Blue (#95CDF7) linear progress bar is the sole animated element on the calm #101417 canvas; all controls are disabled and the permission list fades to 0.4 opacity, giving the PSU a restrained in-progress signal that the AISP revocation is underway and irreversible.

↑↑↑ MOCKUP PROMPT
