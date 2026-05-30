---
ui_yaml_sha: 0a37b7fd9f646c61727fc05be65e3aeffc9773a1b4f8cf66f1064cde39077166
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 1e101d3e0fb7d073a1ca8f00d8949dd3d8f664062095dd05d1d0de1f77250014

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: privacy-policy
state: error
state_visibility: error

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# privacy-policy — error state

> Auto-generated from screens/privacy-policy/ui.yaml @ SHA 10b53bf0f01737d3
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the error state of the Privacy Policy screen for **mifos-x-open-banking**, a professional open banking KMP super-app serving retail banking consumers and field officers.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, error #FFB4AB, outline #8F9285.

**Component 1 — Icon** (48x48dp, centered, 32dp padding from edges): error_state archetype. Material symbol "policy" rendered in error #FFB4AB on surface #12140E. No content rails visible below.

**Component 2 — Text** (full width, centered, 32dp inset): Outfit 16sp, on_surface #E3E3D8. Content: "Unable to load Privacy Policy. Please check your connection and try again."

**Component 3 — Button** (full width minus 32dp inset, 48dp tall, 999dp radius pill, 16dp horizontal padding): Primary Button. Background primary_container #354E16, label "Retry" in on_primary_container #CDEDA3, Outfit 14sp medium. Centered below message with 24dp gap.

Do not use em-dash anywhere in text. Do not make any headline longer than 3 lines or any subtitle longer than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

The error #FFB4AB icon on the near-black #12140E surface communicates failure without aggression, while the primary_container Retry button invites the user back toward restrained stability.

↑↑↑ MOCKUP PROMPT
