---
ui_yaml_sha: 9d40f739969ce84dbe9266a1579a215ad4fff9695ac78689558a182d28d98b69
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 8f3c1a9e7b5d2f0c4a6e8b1d3f7c9a2e5b8d0f4c7a1e3b6d9f2c5a8e1b4d7f

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: pfm-dashboard
state: content
state_visibility: content

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# pfm-dashboard — content state

> Auto-generated from screens/pfm-dashboard/ui.yaml @ SHA aab945f7fcddf2f0
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the pfm-dashboard screen for **HSBC Open Banking**, a regulated UK Open Banking AISP showing Priya Sharma's personal finance overview derived from HSBC transaction data for June 2026.

Archetype: detail_screen

Palette: primary #95CDF7, surface #101417, onSurface #E0E3E8, onSurfaceVariant #C1C7CE, surfaceContainer #1C2024, primaryContainer #004B6F, onPrimaryContainer #C9E6FF, error #FFB4AB, outline #8B9198

1. **Component 1 - Top App Bar** (full width, 56dp): Title "Finances" Outfit titleMedium #E0E3E8 left-aligned on #101417; no back arrow; root tab screen.

2. **Component 2 - Chip Row** (full width minus 32dp, 40dp): Three filter chips horizontal row 36dp height: "This month" selected container #004B6F label #C9E6FF Outfit labelMedium; "Last 3 months" unselected label #C1C7CE on #1C2024; "This year" unselected label #C1C7CE. Chips 8dp gap between.

3. **Component 3 - Stat Block** (full width minus 32dp, 132dp): Net-worth card #1C2024 12dp radius. Label "Total across 3 accounts" labelSmall #C1C7CE. Amount £12,847.33 Outfit displaySmall #E0E3E8 monospace bold. Three compact breakdown rows: Current £4,201.45 in #E0E3E8; Savings £9,845.20 in #E0E3E8; Credit -£1,199.32 in #FFB4AB. Leading label for each in #C1C7CE labelMedium; trailing amount in respective color labelMedium monospace.

4. **Component 4 - Bar Chart** (full width minus 32dp, 200dp): Income vs spending on #1C2024 12dp radius. Header "Income vs Spending" titleSmall #E0E3E8; subtitle "June 2026" labelSmall #C1C7CE. Grouped bars four columns W1 W2 W3 W4 on x-axis labelSmall #C1C7CE: each column income bar #95CDF7 and spend bar #FFB4AB side by side. Heights proportional: W1 £840/£510; W2 £760/£620; W3 £900/£480; W4 £740/£577. Y-axis gridlines #41474D. Net cashflow "+£1,052.45" labelLarge #95CDF7 at card bottom.

5. **Component 5 - List** (full width minus 32dp, top categories): Header "Top categories" titleSmall #E0E3E8 trailing "June 2026" labelSmall #C1C7CE. Seven 48dp rows: category name labelMedium #E0E3E8 leading; spend amount labelMedium monospace trailing; linear progress bar on #41474D below each row. Rows: Groceries £412.30 44pct #95CDF7; Bills £345.00 92pct #FFB4AB; "Dining out" £198.50 38pct #95CDF7; Transport £167.00 62pct #95CDF7; Subscriptions £89.99 75pct #95CDF7; Entertainment £64.75 29pct #95CDF7; Health £28.00 11pct #95CDF7. Text button "View all categories" #95CDF7 below list.

6. **Component 6 - Card** (full width minus 32dp, insights section): Section header "Insights" titleSmall #E0E3E8 above card. Card #1C2024 12dp radius. Row: icon trending_up 24dp #95CDF7 leading; title "Bills up 12 percent" labelMedium #E0E3E8; body "Your bills are higher than last month, mainly from energy. Review your direct debits." bodySmall #C1C7CE two lines.

7. **Component 7 - Chip Row** (full width minus 32dp, 40dp): Three navigation shortcut chips: "By category" with pie_chart icon; "Budgets" with savings icon; "Subscriptions" with autorenew icon. All unselected label #C1C7CE on #1C2024; 36dp height.

8. **Component 8 - Bottom Navigation Bar** (full width, 80dp): Finances tab active icon and label #95CDF7 on #1C2024; Home, Accounts, Settings inactive #C1C7CE.

DO NOT use an em-dash in amounts, category names, insight body, or any chip label. DO NOT write any section header longer than three words or any insight body exceeding 25 words. DO NOT use green for income or red for spending; use #95CDF7 for income bars and credit-positive values, #FFB4AB for spend bars and overbudget rows only. DO NOT render unselected Chip Row chips with a primary-color fill; unselected chips keep #C1C7CE label on #1C2024.

Mood: calm financial clarity rendered through a Bar Chart pairing income #95CDF7 against spending #FFB4AB across four weeks on a dark #101417 canvas; every figure legible, every accent purposeful.

↑↑↑ MOCKUP PROMPT
