---
ui_yaml_sha: 0dff95644480441c813a12ec1e4b235c143956736621078e5327ff9fef0397ce
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 1d2eb39e562e5bbba3309b6d10296a814ae397a9582c6db047659db36ab6db07

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: transactions
state: content
state_visibility: content

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# transactions — content state

> Auto-generated from screens/transactions/ui.yaml @ SHA 76c30ae34a628c67
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the transactions screen for **HSBC Open Banking**, a UK AISP app listing HSBC current account transactions grouped by booking date, with credit amounts in primary and debit amounts in error colour.

Palette: primary #95CDF7, onPrimary #00344E, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, surfaceContainerHigh #262A2E, secondary #B7C9D9, error #FFB4AB, outline #8B9198

Archetype: detail_screen

**Component 1 - Top App Bar** (56dp h, full 393dp w): Outfit medium 22sp "Transactions" #E0E3E8 on #101417; leading arrow-back icon 24dp #E0E3E8; no trailing actions.

**Component 2 - Stat Block** (full width minus 32dp, bg #1C2024, 12dp radius, 16dp padding): two stat cells side-by-side; left cell label "Money In" Outfit 12sp #B7C9D9, value monospace "+£3,212.40" Outfit 600 20sp #95CDF7; right cell label "Money Out" Outfit 12sp #B7C9D9, value monospace "-£1,847.65" Outfit 600 20sp #FFB4AB; period subtext "Jun 2026" centred Outfit 12sp #8B9198 below both cells.

**Component 3 - Chip Row** (horizontal scroll, 16dp start, 8dp gap): four filter chips; "All" active bg #95CDF7 label #00344E Outfit 600 14sp; "Money In" bg #1C2024 stroke #41474D label #E0E3E8 arrow-downward icon 18dp; "Money Out" bg #1C2024 stroke #41474D label #E0E3E8 arrow-upward icon 18dp; "Date Range" bg #1C2024 stroke #41474D label #E0E3E8 date-range icon 18dp.

**Component 4 - List** (full width, vertically scrolling): date-group sections with sticky headers; section header "Monday, 30 Jun 2026" Outfit 600 12sp #8B9198 uppercase 16dp left-padding 8dp top-padding; eight List rows per visible group 64dp each, dividers #41474D; per-row spec: category icon circle 40dp bg #262A2E with glyph 20dp #B7C9D9 left 16dp inset; merchant name Outfit 400 16sp #E0E3E8 centre-left; category Chip 28dp h bg #1C2024 stroke #41474D label Outfit 11sp #B7C9D9 inline-right of name; amount Outfit 600 16sp Roboto Mono right 16dp inset, credit #95CDF7 or debit #FFB4AB; sample rows: "Tesco Superstore" debit "-£67.43" Groceries; "TfL Oyster Top-Up" debit "-£20.00" Transport; "Amazon.co.uk" debit "-£29.99" Shopping; "Netflix UK Ltd" debit "-£17.99" Entertainment; "British Gas Payments" debit "-£87.00" Bills; "Pret A Manger" debit "-£6.75" Eating Out; "Costa Coffee" debit "-£4.55" Eating Out; "HSBC SALARY JUN26" credit "+£3,212.40" Income.

**Component 5 - Bottom Navigation Bar** (56dp h, bg #1C2024, full width): "Accounts" active icon account-balance #95CDF7 label #95CDF7; "PFM" icon insights #8B9198; "Consents" icon verified-user #8B9198; "Profile" icon person #8B9198.

DO NOT use an em-dash anywhere in merchant names, categories, or labels. DO NOT render any date-group header or section label longer than three lines. DO NOT apply a light background to date-group headers or any section while the screen stays on #101417. DO NOT display debit amounts in primary #95CDF7 or credit amounts in error #FFB4AB.

Mood: refined and balanced transaction ledger; credit values glow in #95CDF7 against the dark #101417 field, debit values read in calm #FFB4AB, and the density-5 grouped list keeps real HSBC merchant data scannable without visual noise.

↑↑↑ MOCKUP PROMPT
