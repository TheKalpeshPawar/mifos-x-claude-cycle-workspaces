# Visual Specification — Exchange Rates

| Field | Value |
|---|---|
| Feature | fx-rates |
| Flavor | consumer |
| Archetype | dashboard |

---

## Screen Layout

Top-to-bottom component hierarchy on a single scrollable column (background #FCF8FF):

1. **Page title** — "Exchange Rates" headline_large, #1800B1, padding top 24, horizontal 16
2. **Last updated timestamp** — "Rates updated: 14 May 2026, 15:42 UTC" body_small, #757575
3. **Converter card** — White elevated card (elevation 4, radius 16, padding 20, margin horizontal 16)
   - Send amount input (numeric, "1,000", large title_large bold #1800B1)
   - From currency select ("GBP" with GB flag, dropdown chevron)
   - Swap icon button (circular #EDE7FF bg, #1800B1 swap_vert icon, 32px, centered)
   - To currency select ("EUR" with EU flag, dropdown chevron)
   - Converted result ("= 1,167.20 EUR" display_medium bold #1800B1, centered)
   - Rate sub-line ("Rate: 1 GBP = 1.1672 EUR" body_small #757575, centered)
   - "Send this amount" filled button (full width, #1800B1, white text, radius 12)
4. **Divider** (#EEEEEE, margin horizontal 16)
5. **"Popular Pairs" header** — title_medium, #212121, semi-bold
6. **Rate rows** (6 rows, each: white card radius 8, horizontal row space-between):
   - Pair label (body_large, #212121) | Rate value (body_large bold) | Change badge (color-coded)

---

## Components

### Converter Card
- **Position:** Top of scroll, margin horizontal 16, above popular pairs
- **Style:** White background, border_radius 16, elevation 4 (Material shadow), padding 20
- **Send Amount Input:** Large numeric field, background #F5F5F5, radius 8, font 700 title_large #1800B1, keyboard type decimal
- **Currency Selects:** Pill-shaped dropdowns, background #F5F5F5, radius 8, trailing arrow_drop_down icon, flag emoji prefix
- **Swap Button:** 32px circular button, #1800B1 icon on #EDE7FF background, radius 16, padding 8, self-centered in column
- **Result Display:** "= 1,167.20 EUR" — display_medium, weight 700, #1800B1, centered, padding vertical 8
- **Rate Caption:** "Rate: 1 GBP = 1.1672 EUR" — body_small, #757575, centered
- **CTA Button:** Full-width, background #1800B1, white text, label_large, radius 12, padding vertical 14

### Rate Rows (Popular Pairs)
- **Position:** Below converter card and section header, scrollable list
- **Style:** White background, radius 8, padding horizontal 16 vertical 14, margin horizontal 16, bottom margin 2; horizontal layout with space-between alignment
- **Pair Label:** body_large, weight 500, #212121 (e.g. "GBP / EUR")
- **Rate Value:** body_large, weight 600, #212121 (e.g. "1.1672")
- **Change Badge:**
  - Positive: #4CAF50 with arrow_upward icon (e.g. "+0.2%")
  - Negative: #FF5252 with arrow_downward icon (e.g. "-0.1%")
  - Neutral: #9E9E9E with remove icon (e.g. "0.0%")

---

## Interaction Patterns

| Target | Gesture | Result |
|---|---|---|
| send_amount_input | Tap / type | Decimal keyboard opens; converted result updates live on each keystroke |
| from_currency_select | Tap | Currency picker bottom sheet appears |
| to_currency_select | Tap | Currency picker bottom sheet appears |
| swap_currencies_icon | Tap | from/to currencies swap; converted result recalculates |
| rate_row_gbp_eur / rate_row_gbp_usd / etc. | Tap | Pre-fills converter with that pair's currencies |
| send_money_cta | Tap | Navigates to send-money screen passing current amount and currency |

---

## Content Data

| Element | Sample Value |
|---|---|
| Send amount | 1,000 |
| From currency | GBP (British Pound, GB flag) |
| To currency | EUR (Euro, EU flag) |
| Converted result | = 1,167.20 EUR |
| Live rate caption | Rate: 1 GBP = 1.1672 EUR |
| Last updated | Rates updated: 14 May 2026, 15:42 UTC |
| GBP / EUR rate | 1.1672 · +0.2% (green) |
| GBP / USD rate | 1.2834 · -0.1% (red) |
| GBP / JPY rate | 193.45 · +0.4% (green) |
| EUR / USD rate | 1.0993 · -0.3% (red) |
| USD / INR rate | 83.22 · 0.0% (gray) |
| EUR / GBP rate | 0.8568 · -0.2% (red) |

---

## Design Notes

**Color Usage:**
- Primary #1800B1 dominates key brand moments: title, rate result, CTA, swap icon
- Secondary container #EDE7FF used only for swap icon circular background — provides visual pop without overuse
- Rate change colours are semantic: green #4CAF50 (positive), red #FF5252 (negative), grey #9E9E9E (neutral)

**Typography:**
- Title: headline_large (Mifos brand, bold #1800B1)
- Converter result: display_medium weight 700 — the most visually prominent number on screen
- Rate rows: body_large for values, body_small for change badge — clear information hierarchy

**Spacing:**
- Converter card has generous internal padding (20dp) and sits in 16dp horizontal margin creating a floating card feel
- Rate rows use 2dp bottom margin between them, creating a tight connected list below a 16dp section gap
- 8dp vertical padding on the rate change badge aligns it with the row text baseline

**Accessibility:**
- All interactive elements have role and label declared (combobox for currency selects, button for CTA and swap)
- Currency selects read out the full currency name ("British Pound", "Euro") not just the code
- Rate change badges read out "Up 0.2 percent today" rather than "+0.2%" for screen readers
- Converted result reads "Converted amount: 1,167.20 Euros" — numeric values spelled out contextually

*Generated by /idea export | 2026-05-25*
