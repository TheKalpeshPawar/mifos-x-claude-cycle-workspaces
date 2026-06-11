# MOCKUP — Business Insights

**Archetype:** dashboard
**Shell:** Top app bar — title "Business Insights", `arrow_back` navigation icon. No bottom navigation bar.
**Accent:** #4C662B (Earth-green primary). Typography: Outfit. Design system: Material Design 3.

---

## Screen: populated (cash flow + expenses + counterparties)

```
┌─────────────────────────────────────────┐
│ ←  Business Insights                    │  ← M3 TopAppBar, #F9FAEF bg
├─────────────────────────────────────────┤
│  [ TechStart — Business Current GBP ▾ ] │  ← biz_account_selector (assist chip)
│  ‹ Week  Month  Quarter  Year  Custom › │  ← biz_period_selector_row (horizontal scroll)
│  June 2026                               │  ← biz_period_label, body_medium #5C6057
│                                         │
│  ┌─────────────────────────────────┐    │  ← biz_cash_flow_card, surface_container_low
│  │  Money In    Money Out     Net  │    │
│  │  £75000.00   -£26300.00 £48700  │    │  ← title_small bold; Net #4C662B
│  └─────────────────────────────────┘    │
│                                         │
│  Expenses by Category                    │  ← biz_expenses_title, title_small semibold
│  ┌─────────────────────────────────┐    │  ← biz_expense_donut_card
│  │        ╭───────╮                │    │
│  │        │  ◑    │   donut chart  │    │
│  │        ╰───────╯                │    │
│  │  ● Payroll & Contractors -£15516.01  │  ← biz_category_payroll
│  │  ● Tax                   -£8000.00   │  ← biz_category_tax
│  │  ● Rent & Facilities     -£2500.00   │  ← biz_category_rent
│  │  ● Software & Subs        -£450.00   │  ← biz_category_software
│  │  ● Insurance             -£350.00   │  ← biz_category_insurance
│  └─────────────────────────────────┘    │
│                                         │
│  Top Counterparties                      │  ← biz_merchants_title
│  ┌─────────────────────────────────┐    │  ← biz_merchants_card
│  │  Mifos-X-Open-Bank               │    │
│  │  1 payment            -£15000.00 │    │  ← biz_merchant_payroll
│  └─────────────────────────────────┘    │
└─────────────────────────────────────────┘
```

**Layout notes:**
- Background #F9FAEF; cards use surface_container_low, radius 16dp, 20dp horizontal margin, 16dp padding.
- Account selector: M3 assist chip, trailing `expand_more`; tap opens a BUSINESS-accounts-only picker (bottom sheet).
- Period selector: horizontally-scrolling tab row; selecting a period re-derives all figures client-side; a Custom option opens a range picker.
- Cash-flow row: three equal columns; values Outfit/title_small bold; Net rendered in #4C662B.
- Expense donut: chart + legend rows; the Income category is excluded from the donut (expenses only).
- Counterparties: card with one row per top counterparty (name · payment count · total).

---

## Screen: loading (fetch in flight)

```
┌─────────────────────────────────────────┐
│ ←  Business Insights                    │
├─────────────────────────────────────────┤
│  [ TechStart — Business Current GBP ▾ ] │  ← selector + period row stay visible
│  ‹ Week  Month  Quarter  Year  Custom › │
│  June 2026                               │
│  ┌─────────────────────────────────┐    │  ← skeleton card 1 (height 120)
│  └─────────────────────────────────┘    │
│  ┌─────────────────────────────────┐    │  ← skeleton card 2
│  └─────────────────────────────────┘    │
│  ┌─────────────────────────────────┐    │  ← skeleton card 3
│  └─────────────────────────────────┘    │
└─────────────────────────────────────────┘
```

**Layout notes:** account selector, period row and label remain; 3 shimmer skeleton cards (height 120) replace the data cards. Reduced-motion fallback = static placeholders.

---

## Screen: empty (no business accounts)

```
┌─────────────────────────────────────────┐
│ ←  Business Insights                    │
├─────────────────────────────────────────┤
│                                         │
│                🏪                        │  ← storefront icon
│        No business accounts             │
│  Business insights appear once a        │
│  business account is connected to       │
│  your profile.                          │
│                                         │
└─────────────────────────────────────────┘
```

## Screen: no_activity (account selected, no transactions in period)

```
┌─────────────────────────────────────────┐
│ ←  Business Insights                    │
├─────────────────────────────────────────┤
│  [ TechStart — Business Current GBP ▾ ] │  ← selector + period row + label kept
│  ‹ Week  Month  Quarter  Year  Custom › │
│  June 2026                               │
│                🏪                        │  ← storefront icon
│        No activity in this period       │
│  Cash flow for this business account    │
│  will appear once it has transactions   │
│  in the selected period.                │
└─────────────────────────────────────────┘
```

## Screen: error (fetch failed)

```
┌─────────────────────────────────────────┐
│ ←  Business Insights                    │
├─────────────────────────────────────────┤
│        Could not load business          │
│              insights                   │
│  Check your connection and try again.   │
│            [  Retry  ]                   │  ← retry_load
└─────────────────────────────────────────┘
```

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar, title "Business Insights", `arrow_back` — no bottom nav
- [ ] Background #F9FAEF; cards surface_container_low, radius 16dp, 20dp horizontal margin
- [ ] biz_account_selector: assist chip, trailing `expand_more` → BUSINESS-only account picker
- [ ] biz_period_selector_row: horizontal-scroll tab row + Custom range option
- [ ] Cash-flow row: 3 equal columns; values Outfit/title_small bold; Net in #4C662B
- [ ] Expense donut + legend; Income excluded from the donut (expenses only)
- [ ] Top counterparties card: name · payment count · signed total
- [ ] loading: account selector + period kept; 3 skeleton cards (height 120)
- [ ] empty: `storefront` icon + "No business accounts"
- [ ] no_activity: selector kept + `storefront` icon + "No activity in this period"
- [ ] error: message + "Check your connection and try again." + Retry (retry_load)
- [ ] All text Outfit; touch targets ≥ 48dp

---

_Generated by /idea export | 2026-06-11_
