# MOCKUP — Business Insights

**Archetype:** dashboard
**Shell:** Top app bar — title "Business Insights", `arrow_back` navigation icon. No bottom navigation bar.
**Accent:** #4C662B (Earth-green primary). Typography: Outfit. Design system: Material Design 3.

---

## Screen: loading (fetch in flight)

```
┌─────────────────────────────────────────┐
│ ←  Business Insights                    │  ← M3 TopAppBar, #F9FAEF bg, arrow_back
├─────────────────────────────────────────┤
│  [ TechStart — Business Current GBP ▾ ] │  ← biz_account_selector (assist chip, visible)
│  ‹ Week  Month  Quarter  Year  Custom › │  ← biz_period_selector_row (horizontal scroll)
│  June 2026                              │  ← biz_period_label, body_medium, #5C6057
│                                         │
│  ████████████████████████████████████   │  ← skeleton card 1, height 120, surface_container_low
│  ████████████████████████████████████   │     shimmer: motion.short4 (200ms)
│  ████████████████████████████████████   │     reduced-motion fallback: static placeholder
│                                         │
│  ████████████████████████████████████   │  ← skeleton card 2 (height 120)
│  ████████████████████████████████████   │
│  ████████████████████████████████████   │
│                                         │
│  ████████████████████████████████████   │  ← skeleton card 3 (height 120)
│  ████████████████████████████████████   │
│  ████████████████████████████████████   │
│                                         │
└─────────────────────────────────────────┘
```

**Layout notes:**
- Account selector, period row, and period label remain visible during the fetch — the user can switch account or period even while loading.
- Three skeleton cards (height 120), surface_container_low fill, 16dp radius, 20dp horizontal margin. Shimmer animation (motion.short4, 200ms); reduced-motion fallback = static fill placeholders.
- No data cards visible in this state.

---

## Screen: populated (cash flow + expenses + counterparties)

```
┌─────────────────────────────────────────┐
│ ←  Business Insights                    │  ← M3 TopAppBar, #F9FAEF bg
├─────────────────────────────────────────┤
│  [ TechStart — Business Current GBP ▾ ] │  ← biz_account_selector, assist chip
│  ‹ Week  Month  Quarter  Year  Custom › │  ← biz_period_selector_row (horizontal scroll)
│  June 2026                              │  ← biz_period_label, body_medium, #5C6057
│                                         │
│  ┌─────────────────────────────────┐    │  ← biz_cash_flow_card, surface_container_low
│  │  Money In    Money Out    Net   │    │     16dp radius, 16dp padding, 20dp h-margin
│  │  £75000.00  -£26300.00 £48700   │    │     title_small bold; biz_net in #4C662B
│  └─────────────────────────────────┘    │
│                                         │
│  Expenses by Category                   │  ← biz_expenses_title: title_small semibold
│  ┌─────────────────────────────────┐    │  ← biz_expense_donut_card, surface_container_low
│  │        ╭───────╮               │    │     role img; a11y: total + 5 category breakdown
│  │        │  ◑    │  donut chart  │    │
│  │        ╰───────╯               │    │
│  │  ● Payroll & Contractors        │    │  ← biz_category_payroll
│  │                     -£15516.01  │    │
│  │  ● Tax              -£8000.00   │    │  ← biz_category_tax
│  │  ● Rent & Facilities -£2500.00  │    │  ← biz_category_rent
│  │  ● Software & Subs   -£450.00   │    │  ← biz_category_software
│  │  ● Insurance          -£350.00  │    │  ← biz_category_insurance
│  └─────────────────────────────────┘    │
│                                         │
│  Top Counterparties                     │  ← biz_merchants_title: title_small semibold
│  ┌─────────────────────────────────┐    │  ← biz_merchants_card, surface_container_low
│  │  Mifos-X-Open-Bank              │    │     16dp radius, 20dp horizontal margin
│  │  1 payment           -£15000.00 │    │  ← biz_merchant_payroll
│  └─────────────────────────────────┘    │
└─────────────────────────────────────────┘
```

**Layout notes:**
- Background #F9FAEF throughout. Cards: surface_container_low fill, 16dp radius, 20dp horizontal margin, 16dp padding.
- Account selector: M3 assist chip, trailing `expand_more`; tap opens a BUSINESS-scoped account picker (bottom sheet). Only accounts with `Data.Account[].AccountCategory = Business` appear.
- Period selector: horizontally-scrolling chip row. Selecting a period re-derives all figures client-side. Custom opens a date-range picker.
- Cash-flow row: three equal columns (Outfit/title_small, bold). `biz_net` is coloured #4C662B (positive net). Values are DERIVED client-side from the transaction list.
- Expense donut: donut chart + legend list. Income category is excluded from the donut (expenses only). Each legend row: coloured dot + category name + signed amount.
- Top counterparties card: name · payment count · signed total. Counterparty names resolved by precedence: `MerchantDetails.MerchantName` > account holder name > `TransactionInformation`. Never a raw login username.

---

## Screen: empty (no business accounts)

```
┌─────────────────────────────────────────┐
│ ←  Business Insights                    │
├─────────────────────────────────────────┤
│                                         │
│                🏪                       │  ← storefront icon (empty_icon)
│                                         │
│       No business accounts              │  ← empty_message: title_small, #1A1C16, center
│                                         │
│  Business insights appear once a        │  ← empty_detail: body_medium, #44483D, center
│  business account is connected to       │
│  your profile.                          │
│                                         │
└─────────────────────────────────────────┘
```

**Layout notes:**
- No account selector, no period selector — no Business-scoped account exists in the authorised list.
- `storefront` icon centred, followed by heading and detail text. No CTA — the user needs to connect a business account via the bank's consent flow.

---

## Screen: no_activity (account selected, no transactions in period)

```
┌─────────────────────────────────────────┐
│ ←  Business Insights                    │
├─────────────────────────────────────────┤
│  [ TechStart — Business Current GBP ▾ ] │  ← account selector + period row + label kept
│  ‹ Week  Month  Quarter  Year  Custom › │
│  June 2026                              │
│                                         │
│                🏪                       │  ← storefront icon
│                                         │
│      No activity in this period         │  ← empty_message
│                                         │
│  Cash flow for this business account    │  ← empty_detail: body_medium, #44483D, center
│  will appear once it has transactions   │
│  in the selected period.                │
│                                         │
└─────────────────────────────────────────┘
```

**Layout notes:**
- Account selector, period row, and period label remain so the user can switch period or account. Data cards are replaced by the `storefront` icon + message.

---

## Screen: error (fetch failed)

```
┌─────────────────────────────────────────┐
│ ←  Business Insights                    │
├─────────────────────────────────────────┤
│                                         │
│   Could not load business insights      │  ← error_message: body_large, #1A1C16, center
│                                         │
│   Check your connection and try again.  │  ← error_detail: body_medium, #44483D, center
│                                         │
│  ┌─────────────────────────────────┐    │
│  │             Retry               │    │  ← retry_load intent; FilledButton
│  └─────────────────────────────────┘    │     #4C662B fill, #FFFFFF text, Outfit/label_large
│                                         │
└─────────────────────────────────────────┘
```

**Layout notes:** Centred error state — no data components visible. Retry button fires `Retry` intent → transitions back to `loading` and re-dispatches `get_accounts` + `get_transactions`.

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar: #F9FAEF bg, "Business Insights" title, `arrow_back` navigation icon — no bottom nav
- [ ] `biz_account_selector`: M3 assist chip, trailing `expand_more`; BUSINESS-only account picker bottom sheet
- [ ] `biz_period_selector_row`: horizontal-scroll chip row; Week / Month / Quarter / Year / Custom
- [ ] `biz_period_label`: Outfit/body_medium (14sp), #5C6057
- [ ] All data cards: surface_container_low fill, 16dp radius, 16dp padding, 20dp horizontal margin
- [ ] `biz_cash_flow_card`: 3 equal columns; values Outfit/title_small bold; `biz_net` in #4C662B
- [ ] Expense donut card: donut chart + legend rows with coloured dots; Income excluded from the donut
- [ ] Top counterparties card: name · count · signed total; display name resolved per counterparty rule
- [ ] `loading` state: account selector + period row + label visible; 3 skeleton cards height 120, shimmer motion.short4 (200ms), reduced-motion = static
- [ ] `empty` state: `storefront` icon + "No business accounts" title + supporting detail text
- [ ] `no_activity` state: account selector + period row + label visible; `storefront` icon + "No activity in this period"
- [ ] `error` state: error message + detail text + FilledButton Retry (#4C662B bg, #FFFFFF text)
- [ ] All text Outfit typeface. Touch targets min 48dp. Background #F9FAEF.

---

_Generated by /idea export | 2026-06-14_
