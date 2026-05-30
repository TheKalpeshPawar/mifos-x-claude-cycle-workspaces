---
ui_yaml_sha: b89d839e6c9e3be9d2a9ef40cf53bd6b62a21124885037343b404ee39dd8d76d
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 54807197139a5de335f789d28c6b9bded949f98df8016bed4cd0afa47b6e82fc

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: home
state: error
state_visibility: error

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# home — error state

> Auto-generated from screens/home/ui.yaml @ SHA 3013d45ee22baa31
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the error state of the home screen for **mifos-x-open-banking**, a Kotlin Multiplatform open-banking super-app for consumer retail banking and field officer agent banking.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, error #FFB4AB, on_error #690005, error_container #93000A, on_error_container #FFDAD6, background #12140E, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, outline #8F9285.

**Component 1 — App Bar** (full width, 56dp): Outfit medium 20sp "mifos-x-open-banking" in on_surface #E3E3D8; background surface #12140E; no back button.

**Component 2 — Hero** (full width, centered, 200dp vertical space): error_state illustration centered; wifi-off or cloud-error icon 64dp in error #FFB4AB on error_container #93000A circle 96dp; Outfit medium 20sp "Could not load your account data" in on_surface #E3E3D8 below, 16dp gap; Outfit regular 14sp "Check your connection and try again." in on_surface_variant #C5C8BA, max 2 lines; all centered horizontally.

**Component 3 — Card** (full width minus 32dp insets, 56dp, radius 12dp): single action Card on surface_container #1E201A; centered filled button "Retry" Outfit medium 16sp, background primary_container #354E16, label on_primary_container #CDEDA3, height 48dp, min touch target 48dp; 24dp vertical margin above.

**Component 4 — Chip Row** (full width minus 32dp insets, 40dp, radius 999dp): error detail pill in error_container #93000A with Outfit regular 12sp "Account service unavailable" in on_error_container #FFDAD6; single chip, centered.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

The restrained error #FFB4AB on deep surface #12140E signals a recoverable disruption without alarm, keeping the professional trust of this error_state intact while the Retry path stays immediately clear.

↑↑↑ MOCKUP PROMPT
