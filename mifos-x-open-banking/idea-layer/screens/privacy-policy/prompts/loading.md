---
ui_yaml_sha: 0a37b7fd9f646c61727fc05be65e3aeffc9773a1b4f8cf66f1064cde39077166
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 98aae628db67e1d5293bf2828a0771f1fd1b579e9a90ae7cf03364f57af474cc

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: privacy-policy
state: loading
state_visibility: loading

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# privacy-policy — loading state

> Auto-generated from screens/privacy-policy/ui.yaml @ SHA b430a63027f14933
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the Privacy Policy screen for **mifos-x-open-banking**, a professional open banking KMP super-app serving retail banking consumers and field officers.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, error #FFB4AB, outline #8F9285.

**Component 1 — Skeleton** (full width minus 32dp inset, shimmer placeholder, layout-matching): skeleton_screen archetype. Banner-shaped shimmer bar at top, 48dp tall, 8dp radius, surface_variant #44483D with animated wave sweep from left to right on surface #12140E.

**Component 2 — Skeleton** (full width minus 32dp inset, shimmer placeholder): Card-shaped shimmer block, 96dp tall, 12dp radius, surface_container #1E201A. Two inner shimmer lines: title bar 16dp tall and body bar 12dp tall, both surface_variant #44483D.

**Component 3 — Skeleton** (full width minus 32dp inset, shimmer placeholder): Repeat Card shimmer block at same dimensions for sections 2 through 6 (Data Retention, Lawful Basis, Purpose, Third-Party, User Rights). All blocks use identical shim pattern -- no real text visible.

**Component 4 — Skeleton** (full width minus 32dp inset, shimmer placeholder): Final Card shimmer block for DPO Contact section, 80dp tall, three shimmer lines stacked 8dp apart.

Do not use em-dash anywhere in text. Do not make any headline longer than 3 lines or any subtitle longer than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

The pulsing surface_variant #44483D shimmer on the near-black #12140E canvas signals that privacy content is arriving, keeping the professional banking feel calm while data loads.

↑↑↑ MOCKUP PROMPT
