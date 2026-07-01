---
ui_yaml_sha: c2e476dbefd7802fb6020d1e81e73e172adfc88161c6aa03ff0f02d312619ff7
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 22530d79db063e056b31814b36be911e5463ae8ca8d6a4afb9984f8a3d828b8a

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: statement-detail
state: content
state_visibility: content

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# statement-detail — content state

> Auto-generated from screens/statement-detail/ui.yaml @ SHA 26d904237f219615
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the statement-detail screen for **HSBC Open Banking**, a UK AISP reference app rendering a single June 2026 OBReadStatement2 record from an HSBC current account, within the Trust Blue minimalist Material 3 dark system on a 393x852dp Pixel 5.

Palette: primary #95CDF7, onPrimary #00344E, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, error #FFB4AB, onSurfaceVariant #C1C7CE, outline #8B9198, primaryContainer #004B6F, secondary #B7C9D9

**Component 1 - Top App Bar** (full width, 64dp, bg #101417): back-arrow icon 24dp #95CDF7 left; title Outfit medium 22sp "June 2026 Statement" #E0E3E8; no elevation.

**Component 2 - Card** (full width minus 32dp, 80dp height, r=12dp, bg #1C2024): statement period Outfit regular 14sp "01 Jun 2026 - 30 Jun 2026" #C1C7CE left; Outfit medium 12sp "RegularPeriodic" badge bg #004B6F text #C9E6FF r=full right; 16dp vertical padding.

**Component 3 - Stat Block** (full width minus 32dp, 112dp, r=12dp, bg #1C2024): 2-column grid with 1dp #41474D center divider; left cell "Opening Balance" Outfit regular 12sp #C1C7CE, monospaced bold 18sp "GBP 5,432.18" #95CDF7; right cell "Closing Balance" 12sp #C1C7CE, monospaced bold 18sp "GBP 4,901.47" #95CDF7.

**Component 4 - List** (full width minus 32dp, bg #101417): Outfit medium 12sp "SUMMARY" #8B9198 label 8dp above; 2 rows 56dp each with 1dp #41474D divider; row 1 "Total Credits" 16sp #E0E3E8 left, monospaced "GBP 3,250.00" #95CDF7 right; row 2 "Total Debits" 16sp #E0E3E8 left, monospaced "GBP 3,780.71" #FFB4AB right.

**Component 5 - List** (full width minus 32dp, bg #101417): "FEES" #8B9198 label 8dp above; 1 row 56dp "Account Management Fee" #E0E3E8 left, monospaced "GBP 0.00" #C1C7CE right.

**Component 6 - List** (full width minus 32dp, bg #101417): "INTEREST" #8B9198 label 8dp above; 1 row 56dp "Gross Interest Paid" #E0E3E8 left, monospaced "GBP 0.00" #C1C7CE right.

**Component 7 - List** (full width minus 32dp, bg #101417): "TRANSACTIONS" #8B9198 label 8dp above; 3 rows 64dp each with 1dp #41474D dividers; row 1 "Lloyds Bank - Mortgage" #E0E3E8 left, "15 Jun 2026" #C1C7CE top-right, monospaced "GBP 1,247.00" #FFB4AB bottom-right; row 2 "Salary - Tech Corp" #E0E3E8, "28 Jun 2026" #C1C7CE, monospaced "GBP 3,250.00" #95CDF7; row 3 "Thames Water" #E0E3E8, "22 Jun 2026" #C1C7CE, monospaced "GBP 42.19" #FFB4AB.

**Component 8 - Button** (full width minus 32dp, 52dp height, r=12dp, bg #004B6F, label Outfit medium 16sp "Download PDF statement" #C9E6FF, download icon 20dp #95CDF7 left of label): 24dp below transactions List.

**Component 9 - Bottom Navigation Bar** (full width, 80dp, bg #1C2024): items "Home", "Accounts", "Statements", "More"; "Statements" filled icon #95CDF7; inactive #C1C7CE.

Do not use filled primary #95CDF7 as the download button container; use primaryContainer #004B6F with onPrimaryContainer #C9E6FF label to semantically distinguish the download action. Do not mix credit and debit color semantics; credits monospaced #95CDF7, debits monospaced #FFB4AB, zero figures #C1C7CE throughout. Do not break the dark theme between the header Card and section Lists; all surfaces stay on #101417 or #1C2024 with no white panels. Do not write any headline longer than one line; screen title and section labels are single-line only.

Dense financial detail, perfectly legible. Credit and debit semantics visually distinct. Tone: refined, #95CDF7 minimal.

↑↑↑ MOCKUP PROMPT
