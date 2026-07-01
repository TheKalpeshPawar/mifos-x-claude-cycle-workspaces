---
ui_yaml_sha: 0dff95644480441c813a12ec1e4b235c143956736621078e5327ff9fef0397ce
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 6e92466dd7d8742352ca55a4c3a8506eeb0a4c0b4603e43416da412929bc28dd

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: transactions
state: error
state_visibility: error

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# transactions — error state

> Auto-generated from screens/transactions/ui.yaml @ SHA 401680a91e4c2a42
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the error state of the transactions screen for **HSBC Open Banking**, a UK AISP app showing when the HSBC transaction fetch fails with a recoverable API error on the Open Banking endpoint.

Palette: primary #95CDF7, onPrimary #00344E, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, secondary #B7C9D9, error #FFB4AB, errorContainer #93000A, onErrorContainer #FFDAD6, outline #8B9198

Archetype: error_state

**Component 1 - Top App Bar** (56dp h, full 393dp w): Outfit 22sp "Transactions" #E0E3E8 on #101417; leading arrow-back icon 24dp #E0E3E8.

**Component 2 - Stat Block** (full width minus 32dp, bg #1C2024, 12dp radius, 16dp padding): both cells show placeholder dashes; "Money In" label Outfit 12sp #B7C9D9, value "- -" Outfit 600 20sp #8B9198; "Money Out" label Outfit 12sp #B7C9D9, value "- -" Outfit 600 20sp #8B9198; dimmed appearance, no coloured amounts.

**Component 3 - Error State** (centered, generous vertical padding, bg #101417): error-outline icon 64dp #FFB4AB; title "Could not load transactions" Outfit 600 20sp #E0E3E8; body "HSBC returned an error. Your consent is active; this may be a temporary outage." Outfit 400 14sp #B7C9D9; error-code Banner "HSBC_AIS_40005: Temporary server error" Outfit 12sp #FFDAD6 on bg #93000A 8dp radius 12dp padding 16dp margin-top; Button "Try Again" 48dp full-width bg #95CDF7 label #00344E Outfit 600 14sp 16dp margin-top; 12dp gap between elements.

**Component 4 - Bottom Navigation Bar** (56dp h, bg #1C2024, full width): "Accounts" active icon account-balance #95CDF7 label #95CDF7; "PFM", "Consents", "Profile" each icon and label #8B9198.

DO NOT use an em-dash in any error message or UI label. DO NOT let the error headline or error-code Banner exceed three visible lines. DO NOT lighten the surface or add decorative illustration behind the error icon. DO NOT render any transaction row, date-group header, or Chip Row filter controls in the error state.

Mood: calm and restrained error surface; the #95CDF7 Try Again button anchors recovery without alarm, the #FFB4AB error icon signals the problem clearly on the quiet dark #101417 background.

↑↑↑ MOCKUP PROMPT
