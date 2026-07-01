---
ui_yaml_sha: ac6e434d7320f353f7841e0c17d7c30db5673903d54f2d6da93b8a2edec2a784
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 965383378997c5ce642d50e7bf82144325e03925ad38498ec94cb7e0d2d264f9

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: product
state: empty
state_visibility: empty

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# product — empty state

> Auto-generated from screens/product/ui.yaml @ SHA 30ae9b75ec2edf94
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the empty state of the product screen for **HSBC Open Banking**, a UK Open Banking AISP showing a no-data message when OBReadProduct2 returns an empty product list for this HSBC account.

Palette: surface #101417, primary #95CDF7, onSurface #E0E3E8, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, secondary #B7C9D9, outline #8B9198, primaryContainer #004B6F, onPrimary #00344E

**Component 1 - Top App Bar** (full width, 56dp): static title "Product Details" in #E0E3E8 on #101417; back-navigation arrow left; no shadow.

**Component 2 - Empty State** (centered vertically within remaining 796dp, 393dp wide): line-art icon of an empty document with magnifying glass in #95CDF7, 72dp; heading "No product information" in Outfit 22sp #E0E3E8 centered; body text "HSBC has not shared product details for this account through Open Banking." in Outfit 14sp #C1C7CE centered max 280dp wide; 24dp gap between elements; empty_state archetype.

**Component 3 - Button** (280dp wide, 48dp tall, #95CDF7 fill, 24dp radius): label "Go back" in Outfit 14sp #00344E bold; centered horizontally; 24dp below body text.

**Component 4 - Bottom Navigation Bar** (full width, 56dp, #1C2024 fill): four tabs labeled Accounts, Balances, Party, ATMs; Accounts tab active with #95CDF7 icon and label; inactive tabs in #C1C7CE.

DO NOT use an em-dash anywhere in this mockup. DO NOT render product section rails, credit interest rows, overdraft figures, or shimmer blocks alongside the empty state illustration. DO NOT break the dark surface theme by introducing a light panel or white illustration background. DO NOT place dark text on a dark button background or light text on a light button background.

Quiet #95CDF7 in measured white space. Mood: balanced.

↑↑↑ MOCKUP PROMPT
