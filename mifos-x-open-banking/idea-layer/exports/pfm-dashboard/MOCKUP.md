# MOCKUP — Spending Insights (PFM Dashboard)

**Archetype:** dashboard
**Shell:** Top app bar ("Spending Insights", arrow_back navigation icon, tune action icon) + Bottom nav 5 items (Insights active, #DCE7C8 pill indicator). Typography: Outfit. Design system: M3.
**Accent:** #4C662B (Earth-green primary). Error/alert: #BA1A1A. Warning/pending: #E8A317. Secondary: #386663.

---

## Screen: loading

```
┌─────────────────────────────────────────┐
│ ← Spending Insights              [tune] │  ← Top app bar, #F9FAEF bg
├─────────────────────────────────────────┤
│                                         │
│  Spending Insights                      │  ← headline_large, #4C662B, bold
│                                         │
│  [This Month] [Last Month] [Last 3M] [Custom] →  ← chip row, scroll_horizontal
│  May 2026                               │  ← body_medium, #44483D
│                                         │
│  ┌─────────────────────────────────┐    │
│  │ ████████████████████████████   │    │  ← Skeleton: summary card
│  │ ████████████████████████████   │    │     120dp, #E1E4D5, 20dp radius
│  │ ████████████████████████████   │    │
│  └─────────────────────────────────┘    │
│                                         │
│  ┌─────────────────────────────────┐    │
│  │ ████████████████████████████   │    │  ← Skeleton: budget card
│  │ █████████████████              │    │     120dp, #E1E4D5
│  └─────────────────────────────────┘    │
│                                         │
│  ┌─────────────────────────────────┐    │
│  │                                 │    │  ← Skeleton: pie chart area
│  │      ○○○○○○○○○○○○○○○○○         │    │     220dp circle, #E1E4D5
│  │      ○○○○○○○○○○○○○○○○○         │    │
│  └─────────────────────────────────┘    │
│                                         │
│  ████████  ████████  ████████           │  ← Skeleton: 3 legend rows
│  ████████  ████████  ████████           │
│  ████████  ████████                     │
│                                         │
│  ┌─────────────────────────────────┐    │
│  │ ████████████████████████████   │    │  ← Skeleton: budget progress cards
│  └─────────────────────────────────┘    │
│                                         │
├─────────────────────────────────────────┤
│ [home] [accounts] [insights*] [cards] [more] │  ← Bottom nav, Insights pill active
└─────────────────────────────────────────┘
```

**Layout notes:** Title and period selector always visible during loading. Summary card, budget card, category chart, and budget progress cards shimmer with #E1E4D5 skeletons. shimmer_duration: short4 (200ms). reduced_motion_fallback: static_placeholder.

---

## Screen: populated (content)

```
┌─────────────────────────────────────────┐
│ ← Spending Insights              [tune] │
├─────────────────────────────────────────┤
│                                         │
│  Spending Insights                      │  ← headline_large, #4C662B, bold
│                                         │
│  [This Month✓] [Last Month] [Last 3M] [Custom] →
│  May 2026                               │
│                                         │
│  ┌─────────────────────────────────┐    │  ← Summary card: #FFFFFF, 20dp radius, 2dp elev
│  │  This Month                    │    │  ← title_medium, #1A1C16, semibold
│  │                                 │    │
│  │  Total Spent   Total Received  Net  │
│  │  £1,029.80      £3,200.00   +£2,170.20│  ← title_large; Spent #BA1A1A, Received/Net #4C662B
│  └─────────────────────────────────┘    │
│                                         │
│  ┌─────────────────────────────────┐    │  ← Overall budget card: #CDEDA3 fill, 20dp radius
│  │  Monthly Budget        68% used │    │  ← title_small #4C662B + label_medium #44483D
│  │  £1,029.80 spent    £470.20 left│    │  ← body_medium; spent #1A1C16, left #4C662B
│  │  [████████████████████░░░░░░░░] │    │  ← 10dp progress bar, fill #E8A317, track #E1E4D5
│  │  of £1,500.00 monthly budget   │    │  ← label_small, #44483D
│  └─────────────────────────────────┘    │
│                                         │
│  Spending by Category                   │  ← title_medium, #1A1C16, semibold
│                                         │
│  ┌─────────────────────────────────┐    │  ← Pie chart card: #FFFFFF, 20dp radius, 2dp elev, 220dp h
│  │                                 │    │
│  │        ╭──────────╮             │    │
│  │   ╭────┤ Bills 44%├────╮        │    │  ← Pie segments:
│  │   │    ╰──────────╯    │        │    │    #4C662B Bills 43.7%
│  │   │Food 31%   Trnsp 12%│        │    │    #BA1A1A Food 31.1%
│  │   │Shop 9%    Entmt 4% │        │    │    #386663 Transport 12.1%
│  │   ╰────────────────────╯        │    │    #CDEDA3 Shopping 8.7%
│  │                                 │    │    #E8A317 Entertainment 4.4%
│  └─────────────────────────────────┘    │
│                                         │
│  ● Food & Dining              £320.50   │  ← dot #BA1A1A; body_medium #1A1C16
│  ● Transport                  £125.00   │  ← dot #386663
│  ● Shopping                    £89.30   │  ← dot #CDEDA3
│  ● Bills                      £450.00   │  ← dot #4C662B
│  ● Entertainment               £45.00   │  ← dot #E8A317
│                                         │
│  Budget Progress                        │  ← title_medium, #1A1C16, semibold
│                                         │
│  ┌─────────────────────────────────┐    │  ← Food & Dining card: #FFFFFF, 16dp radius, 1dp elev
│  │  Food & Dining   £320.50/£350.00│    │  ← label #1A1C16; amounts #BA1A1A (near limit 92%)
│  │  [█████████████████████████░░] │    │  ← 8dp bar, #BA1A1A fill, 92%
│  └─────────────────────────────────┘    │
│  ┌─────────────────────────────────┐    │  ← Transport card
│  │  Transport       £125.00/£200.00│    │  ← amounts #44483D (63%)
│  │  [████████████████░░░░░░░░░░░░] │    │  ← #E8A317 fill, 63%
│  └─────────────────────────────────┘    │
│  ┌─────────────────────────────────┐    │  ← Shopping card
│  │  Shopping         £89.30/£150.00│    │  ← amounts #44483D (60%)
│  │  [██████████████░░░░░░░░░░░░░░] │    │  ← #4C662B fill, 60%
│  └─────────────────────────────────┘    │
│  ┌─────────────────────────────────┐    │  ← Bills card
│  │  Bills           £450.00/£500.00│    │  ← amounts #BA1A1A (near limit 90%)
│  │  [█████████████████████████░░░] │    │  ← #BA1A1A fill, 90%
│  └─────────────────────────────────┘    │
│  ┌─────────────────────────────────┐    │  ← Entertainment card
│  │  Entertainment    £45.00/£100.00│    │  ← amounts #44483D (45%)
│  │  [████████████░░░░░░░░░░░░░░░░] │    │  ← #4C662B fill, 45%
│  └─────────────────────────────────┘    │
│                                         │
│         [ Manage Budgets ]              │  ← outlined, #4C662B border + text, 12dp radius
│                                         │
│  Top Merchants                          │  ← title_medium, #1A1C16, semibold
│                                         │
│  ┌─────────────────────────────────┐    │  ← Merchants card: #FFFFFF, 20dp radius, 2dp elev
│  │ [🏪] Tesco          8 txns  £142.30│  ← storefront icon #4C662B on #CDEDA3 circle; amount #BA1A1A
│  │ ─────────────────────────────── │    │  ← divider bottom
│  │ [▶] Netflix         1 txn   £17.99│  ← play_circle #BA1A1A on #CDEDA3; amount #BA1A1A
│  │ ─────────────────────────────── │    │
│  │ [♪] Spotify         1 txn   £11.99│  ← music_note #4C662B on #CDEDA3; amount #BA1A1A
│  │ ─────────────────────────────── │    │
│  │ [🚇] Transport for London        │    │  ← directions_subway #386663 on #DCE7C8
│  │      23 txns              £78.50 │    │  ← amount #BA1A1A; no divider (last row)
│  └─────────────────────────────────┘    │
│                                         │
│          View All Transactions          │  ← text button, #4C662B, label_large, centered
│                                         │
├─────────────────────────────────────────┤
│ [home] [accounts] [insights*] [cards] [more] │
└─────────────────────────────────────────┘
```

**Layout notes:**
- Period chip row horizontally scrollable; selected chip: #4C662B fill + white text; unselected: #CDEDA3 fill + #4C662B text. 20dp pill radius.
- Summary card: 3-column metric row, equal flex. Spent red (#BA1A1A), Received + Net green (#4C662B).
- Overall budget card: #CDEDA3 fill (primary_container). Budget percent label uses #44483D (a11y fix — was #E8A317, contrast FAIL).
- Budget progress bar (overall): #E8A317 fill (warning at 68%). Near-limit categories (Food 92%, Bills 90%): #BA1A1A fill.
- Pie chart: 5 segments with colours matching legend dots. Tap to expand full-screen detail sheet.
- Budget progress tracks: #E1E4D5 (surface_variant). 8dp height for category bars, 10dp for overall bar.
- Merchant icon circles: 40dp, #CDEDA3 (Tesco, Netflix, Spotify), #DCE7C8 (TfL).
- All merchant amounts: #BA1A1A bold (total spend per merchant).
- "Manage Budgets" button centred, outlined style, margin_horizontal: 20dp.

---

## Screen: empty

```
┌─────────────────────────────────────────┐
│ ← Spending Insights              [tune] │
├─────────────────────────────────────────┤
│                                         │
│  Spending Insights                      │
│                                         │
│  [This Month✓] [Last Month] [Last 3M] [Custom] →
│  May 2026                               │
│                                         │
│                                         │
│         [receipt_long icon]             │  ← icon-2xl (48dp), #44483D
│                                         │
│    No transaction history yet           │  ← title_medium, #1A1C16, center
│                                         │
│  Your spending insights will appear     │  ← body_medium, #44483D, center
│  once you have transactions in the      │
│  selected period.                       │
│                                         │
│        [ View Accounts ]                │  ← filled, #4C662B, 12dp radius
│                                         │
│                                         │
├─────────────────────────────────────────┤
│ [home] [accounts] [insights*] [cards] [more] │
└─────────────────────────────────────────┘
```

**Layout notes:** Period selector remains interactive so the user can switch periods. Empty state centred vertically in the content area. "View Accounts" CTA navigates to accounts screen.

---

## Screen: no_budget_set

```
┌─────────────────────────────────────────┐
│ ← Spending Insights              [tune] │
├─────────────────────────────────────────┤
│                                         │
│  Spending Insights                      │
│  [This Month✓] [Last Month] [Last 3M] [Custom] →
│  May 2026                               │
│                                         │
│  ┌─────────────────────────────────┐    │  ← Summary card (full, same as populated)
│  │  This Month                    │    │
│  │  Total Spent   Total Received  Net  │
│  │  £1,029.80      £3,200.00   +£2,170.20│
│  └─────────────────────────────────┘    │
│                                         │
│  Spending by Category                   │
│  ┌─────────────────────────────────┐    │  ← Pie chart (same as populated)
│  │      (pie chart — 5 segments)  │    │
│  └─────────────────────────────────┘    │
│  ● Food & Dining £320.50  ● Transport £125.00
│  ● Shopping £89.30  ● Bills £450.00  ● Entmt £45.00
│                                         │
│  ┌─────────────────────────────────┐    │  ← no_budget_set_banner: #CDEDA3 fill, #E8A317 1dp border
│  │  No budget set                 │    │  ← title_small, #44483D, semibold
│  │                                 │    │
│  │  Set a monthly budget to track  │    │  ← body_small, #44483D
│  │  how much you spend against     │    │
│  │  your target.                   │    │
│  │                                 │    │
│  │        [ Set Budget Now ]       │    │  ← filled, #4C662B, 12dp radius
│  └─────────────────────────────────┘    │
│                                         │
│  Top Merchants                          │
│  ┌─────────────────────────────────┐    │  ← Merchants card (same as populated)
│  │ [🏪] Tesco          8 txns  £142.30│
│  │ [▶] Netflix         1 txn   £17.99│
│  │ [♪] Spotify         1 txn   £11.99│
│  │ [🚇] Transport for London  £78.50 │
│  └─────────────────────────────────┘    │
│          View All Transactions          │
│                                         │
├─────────────────────────────────────────┤
│ [home] [accounts] [insights*] [cards] [more] │
└─────────────────────────────────────────┘
```

**Layout notes:** Budget Progress section and overall budget card are hidden. The no_budget_set_banner replaces them — #CDEDA3 fill with #E8A317 1dp border signals a call-to-action without error severity. Banner title uses #44483D (a11y fix — was #E8A317, contrast FAIL). "Set Budget Now" uses filled primary style.

---

## Screen: error

```
┌─────────────────────────────────────────┐
│ ← Spending Insights              [tune] │
├─────────────────────────────────────────┤
│                                         │
│  Spending Insights                      │
│  [This Month✓] [Last Month] [Last 3M] [Custom] →
│  May 2026                               │
│                                         │
│                                         │
│  ┌─────────────────────────────────┐    │  ← Error banner: white card, 16dp radius
│  │  ⚠ Could not load spending     │    │  ← error_outline icon, #BA1A1A
│  │    insights. Please try again. │    │
│  │                                 │    │
│  │          [  Retry  ]            │    │  ← outlined button, #4C662B
│  └─────────────────────────────────┘    │
│                                         │
│                                         │
├─────────────────────────────────────────┤
│ [home] [accounts] [insights*] [cards] [more] │
└─────────────────────────────────────────┘
```

**Layout notes:** Period selector always visible so the user can switch to a different period as a workaround. Error card centred in content area. Retry triggers `RetryLoad` event → reloads both API endpoints.

---

## Design Checklist (Figma / Stitch)

- [ ] Page title "Spending Insights" — Outfit headline_large (32sp), #4C662B, bold, 20dp horizontal + 16dp top padding
- [ ] Period chip row — horizontally scrollable; min_item_width 80dp; chips 20dp pill radius; selected #4C662B / #FFFFFF, unselected #CDEDA3 / #4C662B
- [ ] Period label "May 2026" — Outfit body_medium (14sp), #44483D, 20dp horizontal + 16dp bottom padding
- [ ] Summary card — #FFFFFF fill, 20dp radius, 2dp elevation, 20dp padding, 20dp margin; 3-column metric row
- [ ] Total Spent "£1,029.80" — Outfit title_large (22sp), #BA1A1A, bold
- [ ] Total Received "£3,200.00" — Outfit title_large, #4C662B, bold
- [ ] Net "+£2,170.20" — Outfit title_large, #4C662B, bold
- [ ] Metric sub-labels (Total Spent / Total Received / Net) — Outfit label_small (11sp), #44483D
- [ ] Overall budget card — #CDEDA3 fill, 20dp radius, 1dp elevation, 20dp padding, 20dp margin
- [ ] Budget percent "68% used" — Outfit label_medium, #44483D semibold (NOT #E8A317 — a11y FAIL)
- [ ] Budget progress bar — 10dp height; #E8A317 fill (68%), #E1E4D5 track, 6dp radius
- [ ] "of £1,500.00 monthly budget" — Outfit label_small, #44483D
- [ ] Category section header — Outfit title_medium (16sp), #1A1C16, semibold
- [ ] Pie chart card — #FFFFFF, 20dp radius, 2dp elevation, 220dp height; 5 segments correctly coloured
- [ ] Legend dots: Food #BA1A1A, Transport #386663, Shopping #CDEDA3, Bills #4C662B, Entertainment #E8A317
- [ ] Legend amounts — Outfit body_medium (14sp), #1A1C16, semibold
- [ ] Budget progress cards — #FFFFFF, 16dp radius, 1dp elevation, 16dp padding, 20dp margin; 8dp height progress bars
- [ ] Near-limit bars (Food & Dining 92%, Bills 90%) — #BA1A1A fill; normal bars — #E8A317 (transport 63%), #4C662B (shopping 60%, entertainment 45%)
- [ ] "Manage Budgets" button — outlined, #4C662B border + text, 12dp radius, 24dp/14dp padding, centred
- [ ] Merchant icon circles — 40dp, #CDEDA3 (Tesco, Netflix, Spotify) or #DCE7C8 (TfL); icon colour: #4C662B (Tesco, Spotify), #BA1A1A (Netflix), #386663 (TfL)
- [ ] Merchant amounts — Outfit body_medium, #BA1A1A, semibold
- [ ] "View All Transactions" — Outfit label_large, text button variant, #4C662B, centred
- [ ] no_budget_set_banner — #CDEDA3 fill, 16dp radius, #E8A317 1dp border; title #44483D (NOT #E8A317); "Set Budget Now" filled #4C662B
- [ ] Loading state — 5 skeleton cards, #E1E4D5, 120dp height, correct radius matching component type
- [ ] Empty state — receipt_long icon (48dp), centred layout, "View Accounts" filled CTA
- [ ] Error state — error card with retry outlined button
- [ ] Bottom nav — 5 tabs, Insights tab active (#DCE7C8 pill indicator), 80dp height
- [ ] Top app bar — "Spending Insights" title, arrow_back navigation icon, tune action icon; #F9FAEF background
- [ ] All text: Outfit typeface. Touch targets 48dp minimum. 16dp horizontal content padding. 8dp grid spacing.

---

_Generated by /idea export | 2026-05-30_
