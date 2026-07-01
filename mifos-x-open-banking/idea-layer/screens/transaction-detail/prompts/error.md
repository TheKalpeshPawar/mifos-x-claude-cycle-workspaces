---
ui_yaml_sha: f9e175a0bb9de365db4c0803b856f44cd0182761536411bcd689e30e8f3ab0d5
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: d8dacb7f543e613fb00b88fd8d62f8afb660879becaeb3e62c34ad62fe8a03ed

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: transaction-detail
state: error
state_visibility: error

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# transaction-detail — error state

> Auto-generated from screens/transaction-detail/ui.yaml @ SHA 77eaa661a339f8b6
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the error state of the transaction-detail screen for **HSBC Open Banking**, a UK AISP app showing when a specific HSBC transaction record cannot be fetched or has been excluded from the active consent scope.

Palette: primary #95CDF7, onPrimary #00344E, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, secondary #B7C9D9, error #FFB4AB, errorContainer #93000A, onErrorContainer #FFDAD6, outline #8B9198

Archetype: error_state

**Component 1 - Top App Bar** (56dp h, full 393dp w): Outfit 22sp "Transaction Detail" #E0E3E8 on #101417; leading arrow-back icon 24dp #E0E3E8; no trailing actions.

**Component 2 - Error State** (centered, generous vertical padding, bg #101417): error-outline icon 64dp #FFB4AB; title "Transaction not available" Outfit 600 20sp #E0E3E8; body "HSBC could not return this transaction record. Consent may have expired or the transaction ID is no longer valid." Outfit 400 14sp #B7C9D9; error-code Banner "HSBC_AIS_40014: Resource not found" Outfit 12sp #FFDAD6 on bg #93000A 8dp radius 12dp padding 16dp margin-top; Button "Try Again" 48dp full-width bg #95CDF7 label #00344E Outfit 600 14sp 16dp margin-top; Button "Go Back" 48dp full-width outlined stroke #41474D label #E0E3E8 Outfit 400 14sp 8dp margin-top.

**Component 3 - Bottom Navigation Bar** (56dp h, bg #1C2024, full width): "Accounts" active icon account-balance #95CDF7 label #95CDF7; "PFM", "Consents", "Profile" each icon and label #8B9198.

DO NOT use an em-dash in any error message or transaction field. DO NOT let the error title exceed three lines or the supporting body text exceed 25 words. DO NOT show a partial transaction Card with placeholder dashes alongside the error in this state. DO NOT colour the error-code Banner in primary #95CDF7 since it represents a failure condition, not an interactive element.

Mood: calm and restrained error view; #95CDF7 anchors the Try Again button as the primary recovery path, and the quiet dark surface keeps the HSBC error code legible without visual alarm.

↑↑↑ MOCKUP PROMPT
