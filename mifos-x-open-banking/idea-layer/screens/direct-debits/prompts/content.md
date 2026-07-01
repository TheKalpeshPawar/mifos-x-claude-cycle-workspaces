---
ui_yaml_sha: 8f627a0862016e34b232d8c97c47bf23a2cebbe6255b04b8f9e6429b85a1f5c9
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: bbd0b5e372c2d2cb454c5ba98119224ddf4b404a0d439431f9476b213107a152

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: direct-debits
state: content
state_visibility: content

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# direct-debits — content state

> Auto-generated from screens/direct-debits/ui.yaml @ SHA 27501988a599e983
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the Direct Debits screen for **HSBC Open Banking**, a UK Open Banking AISP app showing four OBReadDirectDebit2 mandate records for account 40051512345678, sorted Active-first.

Palette: primary #95CDF7, onPrimary #00344E, surface #101417, onSurface #E0E3E8, onSurfaceVariant #C1C7CE, surfaceContainer #1C2024, secondary #B7C9D9, outline #8B9198, error #FFB4AB, primaryContainer #004B6F

**Component 1 - Top App Bar** (56dp, 393dp wide): back-arrow icon in #95CDF7, title "Direct Debits" Outfit Medium 22sp #E0E3E8, container #101417, detail_screen archetype.

**Component 2 - Chip Row** (48dp, 361dp wide, 16dp insets): two read-only filter display chips, 8dp gap. Chip "3 Active" filled container #004B6F label #95CDF7 Outfit Medium 13sp radius 8dp. Chip "1 Inactive" outlined border 1dp #8B9198 label #C1C7CE Outfit Medium 13sp radius 8dp. No interactive toggle; display only.

**Component 3 - List** (scrollable, remaining height, 361dp wide): four Cards stacked 12dp gap, 16dp horizontal insets, Active mandates first then Inactive. Card A (DD-001): container #1C2024 radius 12dp, status badge "Active" background #004B6F label #95CDF7 Outfit Medium 12sp, headline "British Gas" Outfit Medium 16sp #E0E3E8, subline "Last paid GBP 78.00 on 15 Jun 2026" Outfit Regular 14sp #FFB4AB, mandate ref "DD-BG-44120" Outfit Regular 12sp #8B9198. Card B (DD-002): badge "Active" #004B6F / #95CDF7, headline "Vodafone" #E0E3E8, subline "Last paid GBP 29.00 on 20 Jun 2026" #FFB4AB, mandate ref "DD-VF-88301" #8B9198. Card C (DD-003): badge "Active" #004B6F / #95CDF7, headline "Aviva Insurance" #E0E3E8, subline "Last paid GBP 41.50 on 5 Jun 2026" #FFB4AB, mandate ref "DD-AV-10293" #8B9198. Card D (DD-004): badge "Inactive" container #41474D label #C1C7CE, headline "TV Licensing" #E0E3E8, subline "Last paid GBP 13.25 on 1 Mar 2026" Outfit Regular 14sp #C1C7CE muted as mandate is cancelled, mandate ref "DD-TVL-55667" #8B9198.

**Component 4 - Bottom Navigation Bar** (80dp, 393dp wide): container #1C2024, active tab #95CDF7, inactive tabs #8B9198.

Do not use em-dash in any mandate card label, amount subline, or reference field. Do not add a Cancel, Set up, or payment-initiation button; this AISP read-only view cannot modify mandates. Do not place the Inactive TV Licensing card before Active cards; sort order is Active-first per OBReadDirectDebit2 display convention. Do not use green for the Active badge; status signalling must stay within the Trust Blue palette.

Four mandate cards read as calm against the #101417 dark surface, amount lines in #FFB4AB and Active badges in Trust Blue #95CDF7 making the direct debit registry immediately legible.

↑↑↑ MOCKUP PROMPT
