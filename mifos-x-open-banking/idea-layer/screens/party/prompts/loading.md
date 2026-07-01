---
ui_yaml_sha: 30a818627889bd9f5dc82a6ee7b672b5de2bb72e9d847e0b2b417c34501973de
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: f18d32853c5bff7d1f1879d4523bb2804f5c8b1997f29fc99dfe7cd5c71a969d

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: party
state: loading
state_visibility: loading

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# party — loading state

> Auto-generated from screens/party/ui.yaml @ SHA ffe09ebcce2734a9
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the party screen for **HSBC Open Banking**, a UK Open Banking AISP showing shimmer skeleton placeholders block-for-block while OBReadParty2 account-holder identity data fetches from HSBC's API.

Palette: surface #101417, primary #95CDF7, onSurface #E0E3E8, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, secondary #B7C9D9, outline #8B9198, primaryContainer #004B6F, onPrimary #00344E

**Component 1 - Top App Bar** (full width, 56dp): static title "Account Holder" in #E0E3E8 on #101417; back-navigation arrow left; no shimmer on the bar itself; skeleton_screen archetype.

**Component 2 - Card** (full width minus 32dp, 12dp radius, #1C2024 fill): circular shimmer avatar 48dp in #262A2E; to its right two stacked shimmer bars: 160dp x 18dp and 100dp x 14dp; below both a 64dp x 28dp pill shimmer in #262A2E; shimmer gradient sweeps left-to-right; 16dp padding.

**Component 3 - List** (full width minus 32dp): shimmer section-label bar 60dp x 12dp at #262A2E; three 48dp shimmer rows each with 24dp circular icon shard left and 220dp text shard at #262A2E over #1C2024; dividers #41474D.

**Component 4 - List** (full width minus 32dp): shimmer section-label bar 70dp x 12dp; one rectangular card-shaped shimmer 361dp x 96dp with 12dp radius in #262A2E.

**Component 5 - Bottom Navigation Bar** (full width, 56dp, #1C2024 fill): four tab slots in #C1C7CE at 60 percent opacity; no active highlight shown during fetch.

DO NOT use an em-dash anywhere in this mockup. DO NOT render any real name, email address, phone number, or postal address inside shimmer rectangles. DO NOT break the dark surface theme by inserting a white or light panel. DO NOT place dark text on a dark button background or light text on a light button background.

Patient #95CDF7 restraint while identity data arrives. Mood: minimal.

↑↑↑ MOCKUP PROMPT
