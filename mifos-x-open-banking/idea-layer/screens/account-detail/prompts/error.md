---
ui_yaml_sha: 0120895d6ee57bd035a4abe15da76e75865b30a5f02a3bb1e89215c380a564a0
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 122f0ed1619e28b18e1b22069c110c5b0831c8b1f866cbefc3811fbf7d60ab7f

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: account-detail
state: error
state_visibility: error

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# account-detail — error state

> Auto-generated from screens/account-detail/ui.yaml @ SHA 4cebeeffeba2d045
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the error state of the account-detail screen for **HSBC Open Banking**, a UK AISP app showing a recoverable fetch failure when HSBC account data cannot be retrieved via the Open Banking API.

Palette: primary #95CDF7, onPrimary #00344E, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, secondary #B7C9D9, error #FFB4AB, errorContainer #93000A, onErrorContainer #FFDAD6, outline #8B9198

Archetype: error_state

**Component 1 - Top App Bar** (56dp h, full 393dp w): Outfit 22sp "HSBC Current Account" #E0E3E8 on #101417; leading arrow-back icon 24dp #E0E3E8.

**Component 2 - Card** (full width minus 32dp, 12dp radius, bg #1C2024): title "HSBC Advance Current Account" Outfit 600 18sp #E0E3E8; supporting "Sort code: 40-05-15, Acc no: 12345678" Outfit 400 14sp #B7C9D9; meta "GBP · HSBC UK BANK PLC" Outfit 12sp #8B9198; 16dp padding.

**Component 3 - Banner** (full width minus 32dp, 8dp radius, bg #004B6F): shield icon 16dp #95CDF7 inline-left; "Read-only Open Banking access. Your money cannot be moved." Outfit 13sp #C9E6FF.

**Component 4 - Error State** (centered, generous vertical space, bg #101417): error-outline icon 64dp #FFB4AB; title "Unable to load account data" Outfit 600 20sp #E0E3E8; body "HSBC returned an error for account 12345678. Check your consent permissions or try again." Outfit 400 14sp #B7C9D9; error-code Banner "HSBC_AIS_40020: Resource not found" Outfit 12sp #FFDAD6 on bg #93000A 8dp radius 12dp padding; Button "Try Again" 48dp full-width bg #95CDF7 label #00344E Outfit 600 14sp; 24dp spacing between elements.

**Component 5 - Bottom Navigation Bar** (56dp h, bg #1C2024, full width): "Accounts" active icon account-balance #95CDF7 label #95CDF7; "PFM", "Consents", "Profile" each icon and label #8B9198.

DO NOT use an em-dash anywhere in text strings or error messages. DO NOT let the error headline exceed three lines or the supporting body text exceed 25 words in any subtitle. DO NOT shift to a light surface or introduce decorative gradients in the error region. DO NOT display dark text on a dark button or render the Retry button without WCAG AA contrast against the #101417 background.

Mood: restrained and calm error surface; the #95CDF7 Retry button is the single forward path, anchored in a quiet dark field so the HSBC error code reads clearly before the user acts.

↑↑↑ MOCKUP PROMPT
