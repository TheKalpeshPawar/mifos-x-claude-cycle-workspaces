---
ui_yaml_sha: dc51a93dfe2c575708401b94ec0aad258941119f5f0891dc9bcbab82740013cd
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: eeddaada0be5794efccdd36bd9884333d939c64ae7cd7f94e11bc13a3e41b79d

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: consent-detail
state: content
state_visibility: content

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# consent-detail — content state

> Auto-generated from screens/consent-detail/ui.yaml @ SHA 365bd64dbe9adc4f
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the consent-detail screen for **HSBC Open Banking**, a UK AISP app showing full detail for an active account-access consent, including all 11 granted permissions, access dates, and a revoke control, built on Trust Blue minimalist Material 3 DARK on 393x852dp Pixel 5.

Palette: surface #101417, onSurface #E0E3E8, primary #95CDF7, onPrimary #00344E, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, primaryContainer #004B6F

**Component 1 - Top App Bar** (full-width, 64dp): Outfit Medium 22sp "Consent detail" #E0E3E8 on #101417; back-arrow leading; no trailing actions; archetype detail_screen.

**Component 2 - Card** (full-width minus 32dp, 96dp, #1C2024 radius 12dp): HSBC red-hexagon logo 40dp circle leading; Chip "Authorised" filled #004B6F label #95CDF7 right of logo; Outfit Regular 12sp "aac-fb2c4e8a-7d31-4c9e-9f2a-1b3c5d7e9f01" #8B9198 truncated with ellipsis below the logo row.

**Component 3 - Banner** (full-width minus 32dp, 56dp, #004B6F container radius 8dp): event icon 20dp #95CDF7 left; Outfit Regular 13sp "Expires 26 Sep 2026 (89 days remaining)" #C9E6FF; persistent, no dismiss.

**Component 4 - List** (full-width minus 32dp): section label "Access period" Outfit Medium 12sp #C1C7CE uppercase; four List rows 48dp each with leading icon: "Created 28 Jun 2026, 18:25" event icon, "Expires 26 Sep 2026, 00:00" event_busy icon, "Transactions from 30 Mar 2026" history icon, "Transactions to 28 Jun 2026, 23:59" event_available icon; all Outfit Regular 14sp #E0E3E8 on #101417.

**Component 5 - List** (full-width minus 32dp): section label "Data shared" Outfit Medium 12sp #C1C7CE uppercase; 11 List rows 48dp each with check_circle_outline icon #95CDF7 leading: "Account details" supporting "Account identifiers, sort code, account number", "Balances" supporting "Current and available balances", "Transaction history" supporting "Debits and credits with merchant, amount, and date", "Beneficiaries" supporting "Saved payees", "Standing orders" supporting "Scheduled recurring payments", "Direct debits" supporting "Active mandates", "Scheduled payments" supporting "One-off future-dated instructions", "Statements" supporting "Monthly statement metadata", "Product information" supporting "Interest rates and product features", "Account holder name" supporting "Full legal name on the account", "Offers" supporting "Personalised product offers"; labels Outfit Regular 14sp #E0E3E8, supporting Outfit Regular 12sp #C1C7CE.

**Component 6 - Button** (full-width minus 32dp, 48dp): tonal "Revoke access" link_off icon left label Outfit Medium 14sp #E0E3E8 on #1C2024 container radius 24dp; 24dp margin below permissions list.

Do not use em-dash anywhere in labels or body copy. Do not make any headline longer than 3 lines or any subtitle longer than 25 words. Do not break the dark #101417 surface theme between sections by introducing light containers or white backgrounds. Do not place light-coloured text on a light-coloured button, or dark text on a dark button.

The full 11-permission list rendered in check_circle_outline #95CDF7 gives the PSU precise visibility over every data scope; the demoted tonal "Revoke access" button keeps the destructive action accessible but not accidental, delivering a refined and trust-legible consent-detail view.

↑↑↑ MOCKUP PROMPT
