---
ui_yaml_sha: 0dff95644480441c813a12ec1e4b235c143956736621078e5327ff9fef0397ce
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 906d174c13ca1b7661d1f049d963fb42274a3c095edaf99589958c3bc7eee052

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: transactions
state: empty
state_visibility: empty

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# transactions — empty state

> Auto-generated from screens/transactions/ui.yaml @ SHA 3769e5021574d113
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the empty state of the transactions screen for **HSBC Open Banking**, a UK AISP app showing when no HSBC transactions match the active filter or none have been returned for the selected account and date range.

Palette: primary #95CDF7, onPrimary #00344E, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, secondary #B7C9D9, error #FFB4AB, outline #8B9198

Archetype: empty_state

**Component 1 - Top App Bar** (56dp h, full 393dp w): Outfit 22sp "Transactions" #E0E3E8 on #101417; leading arrow-back icon 24dp #E0E3E8.

**Component 2 - Stat Block** (full width minus 32dp, bg #1C2024, 12dp radius, 16dp padding): both stat cells dimmed; "Money In" label Outfit 12sp #B7C9D9, value "£0.00" Outfit 600 20sp #8B9198; "Money Out" label Outfit 12sp #B7C9D9, value "£0.00" Outfit 600 20sp #8B9198; period subtext "Jun 2026" centred Outfit 12sp #8B9198; no coloured amounts rendered.

**Component 3 - Chip Row** (horizontal scroll, 16dp start, 8dp gap): four chips; "Money In" active bg #95CDF7 label #00344E Outfit 600 14sp arrow-downward icon 18dp; "All", "Money Out", "Date Range" each bg #1C2024 stroke #41474D label #E0E3E8.

**Component 4 - Empty State** (centered, generous vertical padding, bg #101417): receipt-long icon 64dp #41474D; title "No transactions found" Outfit 600 20sp #E0E3E8; body "No money-in transactions for Jun 2026. Try a different filter or expand your date range." Outfit 400 14sp #B7C9D9; Button "Clear Filters" 48dp full-width bg #95CDF7 label #00344E Outfit 600 14sp; 24dp element gap between icon, title, body, and button.

**Component 5 - Bottom Navigation Bar** (56dp h, bg #1C2024, full width): "Accounts" active icon account-balance #95CDF7 label #95CDF7; "PFM", "Consents", "Profile" each icon and label #8B9198.

DO NOT use an em-dash in any label or body text. DO NOT make the empty-state headline longer than three lines or any supporting subtitle longer than 25 words. DO NOT change the surface colour mid-screen or introduce a decorative pattern in the empty region. DO NOT colour the empty-state icon in primary #95CDF7 since it represents absence, not an active element.

Mood: calm and minimal empty view; the single #95CDF7 call-to-action Button stands clearly against the quiet dark field, guiding the user back toward a broader HSBC filter.

↑↑↑ MOCKUP PROMPT
